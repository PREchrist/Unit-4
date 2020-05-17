Defibrillator in Codingame by Javascript

The city of Montpellier has equipped its streets with defibrillators to help save victims of cardiac arrests. The data corresponding to the position of all defibrillators is available online.

Based on the data we provide in the tests, write a program that will allow users to find the defibrillator nearest to their location using their mobile phone.
 	Rules
The input data you require for your program is provided in text format.
This data is comprised of lines, each of which represents a defibrillator. Each defibrillator is represented by the following fields:
A number identifying the defibrillator
Name
Address
Contact Phone number
Longitude (degrees)
Latitude (degrees)
These fields are separated by a semicolon (;).

Beware: the decimal numbers use the comma (,) as decimal separator. Remember to turn the comma (,) into dot (.) if necessary in order to use the data in your program.
 
DISTANCE
The distance d between two points A and B will be calculated using the following formula:


​
Note: In this formula, the latitudes and longitudes are expressed in radians. 6371 corresponds to the radius of the earth in km.

The program will display the name of the defibrillator located the closest to the user’s position. This position is given as input to the program.
 	Game Input
Input
Line 1: User's longitude (in degrees)

Line 2: User's latitude (in degrees)

Line 3: The number N of defibrillators located in the streets of Montpellier

N next lines: a description of each defibrillator


```.js
const longtitudeA = parseFloat(readline().replace(',', '.'));
const latitudeA = parseFloat(readline().replace(',', '.'));
const N = parseInt(readline());
let defibs = [];
let minDestination = Infinity;
let nearestPoint = -1;
let x = 0;
let y = 0;
let d = 0;
let longtitudeB = 0;
let latitudeB = 0;

for (let i = 0; i < N; i++) {
    defibs[i] = readline().split(';');
    defibs[i][4] = parseFloat(defibs[i][4].replace(',', '.'));
    defibs[i][5] = parseFloat(defibs[i][5].replace(',', '.'));
    
    longtitudeB = defibs[i][4];
    latitudeB = defibs[i][5];
    x = (longtitudeB - longtitudeA) * Math.cos((latitudeA + latitudeB)/2);
    y = latitudeB - latitudeA;
    d = Math.sqrt(Math.pow(x, 2) + Math.pow(y, 2)) * 6371;
    
    if (d < minDestination) {
        minDestination = d;
        nearestPoint = i;
    }
    printErr(`${i}: ${x}, ${y}, ${d}, ${minDestination}, ${nearestPoint}`);
}

print(defibs[nearestPoint][1]);
```
![defribillator](Defribillator.png)
