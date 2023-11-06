# Impresora_3D

El presidente de la sección de URE de Madrid Cesar Gallego EA4HFF, Nos donó el Jueves 21 de Septiembre de 2023:
- La impresora 3D, Creality CR-30.
- 3DPrintMill (CR-30) Extended Bracket, el cual permite imprimir piezas más grandes.
- Más un rollo de PLA de 1Kg.

La idea todavía por desarrollar es descargar un progrma an una raspberry-pi para poder enviar los archivos por internet, y dado que el eje z es infinito no es necesario estar pendiente de quitar las piezas, limpiar o echar la laca, como puede ocurrir en otras impresoras.

El programa necesario para diseñar las piezas, consiste en instalar cualquier programa que permita exportar la pieza en cuestión en un archivo .stl. Yo recomiendo SolidEdge (https://solidedge.siemens.com/es/solutions/users/students/) por ser un programa profesional, pero que permite tener una versión de estudiante sin limitaciones. Aunque pueden existir otros que os sirvan u os entendáis mejor.

Para generar los archivos GCODE, se necesita un programa especial, que permita fraccionar la piezas en comando entendibles por la impresora, uno de los más conocidos para este fin es el "CURA". Sin embargo dado que el ángulo de extrusión es de 45º, se necesita un programa especial para poder generar los archivos .GCODE. Existen diversos programas para ello, que se pueden encontrar en la página oficial de creality https://www.creality.com/pages/download-cr-30-3d-printer. Sin embargo dentro de esos el que más recomendamos es Software and Drive_3DPrintMill. El cual es una adaptación directa de el "CURA".

Es importante que cuando se instala este programa, por defecto cuando termina una pieza deja el extrusor pegado a la cama, y dado que se queda caliente tiende a dejar una marca y quemarla. Es por ello que se necesita modificar el codigo de la propia impresora; para ello Settings->Printers->Manage Printers-> Y en la impresora que hayas definido en machine settings->End Gecode y escribir lo siguiente:

"G1 Y15
G92 E0   ; Set Extruder to zero
G1 E-6   ; Retract 6mm
G92 Z0   ; Set Belt to zero
G1 Z15   ; Move Belt 15mm before starting up the next product
G92 Z0   ; Set Belt to zero again

;˄˄˄˄˄˄˄˄˄˄˄˄˄˄˄˄ - copy up to here / paste codes just above here - ˄˄˄˄˄˄˄˄˄˄˄˄˄˄˄˄

G1 Y15
M104 S0  ; Extruder heater off
M140 S0  ; Heated bed heater off
M106 S0  ; Part cooling fan off
M106 P1 S0  ; Rear fan off
G92 Z0
G1 Z10 F1000
G28 X0 F2000
G1 Z20 F1000
G1 X170 F2000
M18      ; Disable all stepper motors"

Ruben Sanz Sanchez EA1FRA
