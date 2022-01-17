# Donnees-lycees
Traiter des donnees
import bs4
import urllib
import wget
import shutil
import PyPDF2
   


def get_pdfs_Poitier():
    my_url = "https://www.ac-poitiers.fr/minihome/publications-statistiques-122378"
    links = []
    html = urllib.request.urlopen(my_url).read()
    html_page = bs4.BeautifulSoup(html, features="lxml") 
    og_url = html_page.find("meta",  property = "og:url")
    base = urllib.request.urlparse(my_url)
    for link in html_page.find_all('a'):
        current_link = link.get('href')
        if current_link.endswith('download'):
            if og_url:
                print("currentLink",current_link)
                links.append("https://www.ac-poitiers.fr" + current_link)
            else:
                links.append(base.scheme + "://" + base.netloc + current_link)

   
    
    file1 = wget.download(links[1])
    shutil.move("./" + file1, "../data/" + file1)
    pdf1 = open("../data/" + file1, "rb")
    pdfReader = PyPDF2.PdfFileReader(pdf1) 
    print(pdfReader.numPages)
    pageObj = pdfReader.getPage(1)  
    test = pageObj.extractText()
    print(test)
    pdf1.close()  

    

    
def get_pdfs_Bordeaux():
    my_url = "https://www.ac-bordeaux.fr/article/second-degre-121965"
    links = []
    html = urllib.request.urlopen(my_url).read()
    html_page = bs4.BeautifulSoup(html, features="lxml") 
    og_url = html_page.find("meta",  property = "og:url")
    base = urllib.request.urlparse(my_url)
    for link in html_page.find_all('a'):
        current_link = link.get('href')
        if current_link.endswith('download'):
            if og_url:
                print("currentLink",current_link)
                links.append("https://www.ac-bordeaux.fr" + current_link)
            else:
                links.append(base.scheme + "://" + base.netloc + current_link)

def get_pdfs_Limoges():
    my_url = "https://www.ac-bordeaux.fr/article/second-degre-121965"
    links = []
    html = urllib.request.urlopen(my_url).read()
    html_page = bs4.BeautifulSoup(html, features="lxml") 
    og_url = html_page.find("meta",  property = "og:url")
    base = urllib.request.urlparse(my_url)
    for link in html_page.find_all('a'):
        current_link = link.get('href')
        if current_link.endswith('download'):
            if og_url:
                print("currentLink",current_link)
                links.append("https://www.ac-bordeaux.fr" + current_link)
            else:
                links.append(base.scheme + "://" + base.netloc + current_link)

   
    
    file2 = wget.download(links[0])
    shutil.move("./" + file2, "../data/" + file2)


    

#programe de creation de la page html

fichier = open("test")
texte = fichier.read()



def write_html_header(fichier, titre):
    fichier.write("<?xml version=\"1.0\" encoding=\"UTF-8\" ?>\n")
    fichier.write("<!DOCTYPE html>\n")
    fichier.write("<html xmlns=\"http://www.w3.org/1999/xhtml\" xml:lang=\"fr\" lang=\"fr\" dir=\"ltr\">\n")
    fichier.write("<style>\n")
    fichier.write("table, th, td {\n")
    fichier.write("border:1px solid black;")
    fichier.write("}\n")
    fichier.write("</style>")
    
    fichier.write("\t <head>\n")
    fichier.write(("\t\t<title>"+titre)+"</title>\n")
    fichier.write("\t </head>\n")
    
def write_html_body_begin(fichier):
    fichier.write("<body>\n")
    
def write_html_body_end(fichier):
    fichier.write("</body>\n")

    
def write_html_body(fichier):
    fichier.write("Blablabla...\n")
    
    
def write_html_table(fichier, colonne1, colonne2):
    
    fichier.write("<table>\n")
    fichier.write("<tr>")
    fichier.write("\t<th> Titre colonne1 </td>")
    fichier.write("\t<th> Titre colonne1 </td>")
    fichier.write("\t</tr>\n")
    for i in range(len(colonne1)):
         fichier.write("<tr>")
         fichier.write("\t<td>"+str(colonne1[i])+"</td>")
         fichier.write("\t<td>"+str(colonne2[i])+"</td>")
         fichier.write("\t</tr>\n")
    fichier.write("</table>\n")
    fichier.write(texte)
def write_html_end(fichier):
    fichier.write("</html>")
    
fichier = open("fichier.html", "w")
write_html_header(fichier,"Mon titre")
write_html_body_begin(fichier)
#write_html_body(fichier)
colonne1 = [1, 2, 3]
colonne2 = [4, 5, 6]
write_html_table(fichier, colonne1, colonne2)
write_html_body_begin(fichier)
write_html_end(fichier)


fichier.close()
