#definisco le variabili immagine
lato=50
immagine=lato*10


def setup():
    #definisco foglio
    background(255)
    size(immagine,immagine)
    messaggio=[]             #variabile che conterra' il messaggio
    messaggio= input('inserire la frase da codificare')
    print(messaggio)
    codifica(messaggio)
    
def input (frase=''):
    #funzione che prende in input il messaggio digitato
    from javax.swing import JOptionPane
    return JOptionPane.showInputDialog(frame,frase)
                        
    
def codifica(messaggio):
    #funzione che si occupa di convertire i caratteri ed inserire i
    #rispettivi codici ascii in un array
    i=0                      #indice messaggio
    lung=len(messaggio)      #lunghezza messaggio
    arrayascii=[]            #array codici ascii
    while (i<lung):       
        singolo=ord(messaggio[i])      #variabile di appoggio
        arrayascii.append(singolo)     #aggiungo alla lista

        i+=1
    create(arrayascii)
    
        
        
def create(arrayascii):
    global lato, immagine
    i=0
    px=0                #indice x per colore
    py=0                #indice y per colore
    lunghezza=0         #indice pixel
    loadPixels()        #dispongo i pixel su un array
    
    while (i<len(arrayascii)+1): #scorre tutto l'array di codici ascii
        if (i!=-1): 
            #se esiste il primo inserisco in r e verifico il successivo             
            r=arrayascii[0]
            if (i+1!=-1):
                #se esiste inserisco in g e verifico il successivo
                g=arrayascii[1]
                if (i+2!=-1):
                    #se esiste inserisco in b
                    b=arrayascii[2]
                else:
                    #se non esiste
                    b=255
            else:
                #se non esiste allora non esiste il successivo
                g=255
                b=255
        else:
            #se non esiste allora non esistono i successivi
            r=255
            g=255
            b=255
        
        #riempio il pixel
        for px in range (lato):
            for py in range (lato):
                pixels [lunghezza+py+(immagine*px)]=color (r,g,b)
        
        lunghezza=lunghezza+lato
        i=i+1
    
        
        #elimino la prima tripletta per lavorare sulla successiva
        del(arrayascii[:3])
        
        #se termina la prima riga matrice
        if (lunghezza%immagine==0):
            lunghezza=lunghezza+immagine*(lato-1) 
 
        
    #completo con i pixel neri
    while (lunghezza%immagine!=0):
        for px in range (lato):
            for py in range (lato):
                pixels[lunghezza+py+immagine*px]=color(0,0,0)
        lunghezza+=lato
    updatePixels()  
    save("code.tiff")

