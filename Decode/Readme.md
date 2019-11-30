#definisco le variabili immagine
lato=50
immagine=lato*10


def setup():
    #creo il foglio e prendo in input l'immagine
    
    global img
    size(immagine,immagine)
    img=loadImage("code.tiff")
    
    decodifica()
    
def decodifica():
    img.loadPixels()     #dispongo i pixel su un array
    messaggio=""         #stringa messaggio
    p=0                  #indice pixel
    color1=0             #r
    color2=0             #g
    color3=0             #b
    
    #scorro finche' il pixel successivo non e' nero
    while (img.pixels[p]!=color(0,0,0)):
        #converto i codici carattere r, g, b e li inserisco nelle variabili    
        r=red(img.pixels[p])              
        g=green(img.pixels[p])
        b=blue(img.pixels[p])
        color1=chr(int(r))
        color2=chr(int(g))
        color3=chr(int(b))
        
        #aggiungo i caratteri alla stringa
        messaggio=messaggio+color1+color2+color3
        
        #pixel successivo
        p+=lato
        
        #se sono al termine della riga matrice passo alla successiva
        if (p%immagine==0):
            p=p+immagine*(lato-1)
    
    
    
    print(messaggio)   
    image(img,0,0)
