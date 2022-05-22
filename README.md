# RenderGPU
Segona pràctica de GiVD 2021-22

::

    Aquest és el model base del README.rst que huarue d'omplir com a documentació de la pràctica. De cara a ala presentació d'qeust document, si us plau, esborreu les notes i aquest text. 
    
**Abstract**

En aquest pràctica hem fet primerament la migració de les dades reals i virtuals traspasant les classes corresponents a la creació d'objectes, i lectura de fitxers. Mentres feiem aquesta feina, a l'hora també creàvem les llums i materials per separat, comprovant que funcionés de manera correcte. Un cop tot funcional ho hem juntat creant les llums i materials dins de les classes que creen les escenes virtuals i reals. 

Dit això, hem passat a crear els shaders demanats comprovant que funcionen tant per la lectura d'objectes com d'escenes, passant les dades entre CPU i GPU i activant-los en temps d'execució. I per finalitzar, hem implementat les textures pels objectes llegint els seus téxels i mostrant-los en el propi objecte.

**Features**

*(NOTA: Quines parts heu desenvolupat i qui ho ha fet de l'equip. Editeu la llista que teniu a continuació afegint darrera de cada punt, la persona que ha treballat en aquell punt.) *

- Fase 1
    - Adaptació a la lectura de fitxers de dades
        - [X] Objectes
        - [X] Escenes virtuals - Jordi Bujaldon
        - [X] Escenes de dades Reals - Ivan Mansilla
    - Material
    - Light
        - [X] Puntual - Lluc Slatosch
        - [ ] Direccional
        - [ ] Spotlight
        - [X] Ambient Global - Lluc Slatosch
    - Shading
        - [X] Depth - Jordi Bujaldon
        - [X] Phong - Lluc Slatosch
        - [X] Gouraud - Jordi Bujaldón
        - [X] Toon-shading - Lluc Slatosch
    - Textures
        - [X] Textura com material en un objecte -  Miriam Martínez
        - [ ] Textura al pla base
        

- Fase 2 
    - [ ] Èmfasi de siluetes
    - [ ] Mapping indirecte de textures
    - [X] Animacions amb dades temporals - Miriam Martinez
    - [ ] Normal mapping
    - [ ] Entorn amb textures
    - [ ] Reflexions
    - [ ] Transparències via objectes.
    - [ ] Transparències via environmental mapping.


**Extensions**

**Memòria**

ESCENES VIRTUALS:
En aquesta part, primer hem creat la classe AbstractFactoryScenes encarregada de crear els dos tipus d'escenes que tenim, en aquest cas la virtual. A més, hem implementat el mètode que crea l'escena (createScene). Dins d'aquest mètode el que fem es llegir l'escena passada pel fitxer .json creant els objectes i els materials demanats. Un cop l'escena s'ha creat, li hem afegit una llum puntual per donar-li la il·luminació necessaria, i seguidament hem emitit un senyal passant-li la nova escena de manera que s'actualitzarà l'escena amb les propietats de la nova.

ESCENES DE DADES REALS:

LLUMS:
No va suposar grans problemes implementar la laprt de llums. Pràcticament tot el necessari apareixia a l'enunciat. Al principi no sabia com canviar els valors desde la mainWindow. Havia de passar les llums a la GPU cada cop que el MainWindow crida al mètode setLights del GLWidget, és a dir, posar el lightsToGPU a setLights.
La llum ambient global era pràcticament el mateix, i la direccional la vaig deixar per més endavant, pero finalment no he tingut temps d'implementarla, ja que tampoc l'hi teniem a la P1. Els shaders estàn implementats com per funcionar amb una sola llum, ja que no hem pogut afegir-ne més a la MainWindow. Encara així, per al shader bàsic, si construím fins a 5 llums, les interpretarà bé i podrà treure el color de qualsevol de les Id(per exemple). Veure captura de pantalla on apareix el cub turquesa fosc, la llum 1(modificable) té els seus valors Id a 0, i les altres dues tenen per defecte verd i blau. Treiem la suma de les 3 id com a color i es veu el turquesa.
S'han modificat els valors per defecte de la MainWindow, ja que apareixia en un verd extrany.


SHADING:
Primerament hem implementat el Depth Shading. Aquest shader només necessita la distància del vèrtex a la càmera, i per això hem fet servir el gl_FragCoord.z, que és la distància demanada. Per a que es veiés en intensitats segons la distància, hem hagut de calcular la intensitat del color segons la distància fent que aquest sigués el color del píxel.
Després hem calculat el Gouraud Shading. En aquest cas havíem de calcular les normals dels vèrtexs per més tard calcular el color. En la lectura dels objectes, hem llegit els vèrtexs i les normals passant-los directament al vèrtex shader. Dins del vèrtex shader hem calculat el color del píxel fent el Blinn Phong, i aquest color és el que li passem al fragment shader per a que mostri el color del píxel.
A continuació hem fet el Phong Shading. Aquest és molt semblant al Gouraud però en comptes de calcular el Blinn Phong dins del vèrtex ho hem fet en el fragment shader.
I per finalitzar la part de shading, el qual no ha suposat grans problemes després de fer Phong i Gouraud. Simplement era fer uns quants if's on segons el prodcucte escalar de la normal i la direccio de la llum posem un valor més o menys fosc de la id. La direcció de la llum, al no tenir llums direccionals, la agafem com a la L.

TEXTURES:

**Screenshots**

3 llums:

![3llums](https://user-images.githubusercontent.com/32061294/169720431-21f9f9cd-f839-4bd6-b778-eb4f4b59bffa.png)

Jupiter:

![jupiter](https://user-images.githubusercontent.com/32061294/169720129-978c1f2a-82c1-4019-a567-92e970c7bc9c.png)

Textures:

![bricks](https://user-images.githubusercontent.com/32061294/169720166-a5f58681-f79b-49f5-bb9a-e22cfbc4cb48.png)

Blinn Phong:

![phong](https://user-images.githubusercontent.com/32061294/169720172-c3ee132c-a784-41e0-9634-4bb97c3bd6f6.png)

Toon shading:

![toon](https://user-images.githubusercontent.com/32061294/169720179-c2274453-542b-4831-85d5-e52eb2ce5e0e.png)

Depth shading:

![depth-shading](https://user-images.githubusercontent.com/32061294/169720183-ef3d46fe-e4df-4431-a334-cdbaeccd87f8.png)

Gouraud:

![gouraud-escena-virtual](https://user-images.githubusercontent.com/32061294/169720202-ef21ce48-1298-49f5-9647-3ecf797f73fc.png)


**Additional Information**

Un dels principals problemes que hem tingut ha estat el temps de dedicació a la pràctica degut a la càrrega de feina que ha hagut en l'últim mes. A més, hem tingut molts problemes en la part de l'escena de dades reals.
