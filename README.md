    def CreateLabyrinth(self):                                        #Fonction de création du labyrinthe
        departx=self.terminal_state//self.width                       #initialisation du point de départ des branches
        departy=self.terminal_state%self.width
        height=self.height
        width=self.width
        init=0                                                        #init va correspondre au nombre de boucles minimums à effectuée
        L=np.zeros((height,width))                                    #initialisation du labyrinthe
        i=[departx,departx]                                           
        j=[departy,departy]                                           #initialisation des indices correspondants aux extrémités de notre branche
        L[i[0]][j[0]]=1                                               #Case de départ est accesbile
        for c in range (width-2*departx):           #Creation d'un chemin entre la case d'arrivée du labyrinthe et sa case opposée
            L[width-i[0]-c][j[0]]=1
        i[1]=width-departx                          #mise à jour de la position des extrémités de la branche
        for b in range (height-2*departy):
            L[i[1]][height-j[0]-b]=1
        j[1]=height-depart
        Stop=[False,False]                                            #initialisation condition d'arrêt                           
        choice=[random.randint(0,3),random.randint(0,3)]              #choix des directions pour les nouveaux chemins qui vont être crées:Chaque nouveau chemin partira d'une extrémité différente de la branchre 
        count=0                                                       #Nombre de cases blanches placées (sans compter le chemin initiale)
        while Stop!=[True,True]:                                      #Début de la boucle permettant les créations des chemins
            for b in range (2):                                       #Faire pour les 2 extrémités du labyrinthe
                if choice[b]==0:                                      #Cas création d'un chemin à gauche
                    for a in range  (1,random.randint(3,random.randint(3,width//5))):  
                        if j[b]-1<0  :
                            Stop[b]=True
                        else:
                            L[i[b]][j[b]-1]=1
                            j[b]=j[b]-1
                            count+=1      
                if choice[b]==1:                                      #Cas création d'un chemin à droite
                    for a in range (1,random.randint(3,random.randint(3,width//5))):
                        if j[b]+1>width-1 :
                            Stop[b]=True
                        else:
                            L[i[b]][j[b]+1]=1
                            j[b]=j[b]+1
                            count+=1
                if choice[b]==2:                                      #Cas création d'un chemin vers le haut
                    for a in range  (1,random.randint(3,random.randint(3,width//5))):
                        if i[b]-1<0:
                            Stop[b]=True
                        else:
                            L[i[b]-1][j[b]]=1
                            i[b]=i[b]-1
                            count+=1
                if choice[b]==3:                                      #Cas création d'un chemin vers le bas
                    for a in range  (1,random.randint(3,random.randint(3,width//5))):
                        if i[b]+1>height-1 :
                            Stop[b]=True
                        else:
                            L[i[b]+1][j[b]]=1
                            i[b]=i[b]+1
                            count+=1
            if Stop!=[True,True]:                                     
                Stop=[False,False]                                    #réinitialisation à 0 de Stop s'il n'y a pas l'arrêt de la boucle
                init=init+1                                           #Mise à jour du nombre de boucles déjà effectués
            if init<height:                                           #Si le nombre de boucle effectués est inférieur à un certain nombre, réinitialisation à 0 de Stop
                Stop=[False,False] 
                init=init+1
            choice=[random.randint(0,3),random.randint(0,3)]  
                    #Choix des nouvelles directions pour la prochaine boucle
            if count>height*width//4:                                 #Si le nombre de cases accessibles dépasse ce nombre, arêt de la boucle
                Stop=[True,True]  
        M=[]                                                          #remise en Liste du labyrinthe
        for d in range (height):
            for l in range (width):
                M.append(L[d][l])
        return(M)
