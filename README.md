# Cypress Random Tester (Monkey)
This repository contains the code for a random tester developed using [Cypress](https://www.cypress.io/). Two versions are developed, including a full random tester and a smarter random tester, and the differences between these two remain in the type of commands that each can execute. The detail is explained in sections below

## How to run
In order to use the tester, you will have to follow these steps:
- Get the source code from this repository: Click on Download as Zip and unzip the folder in your machine or clone the repo
- Install the required modules: Using [Node Package Manager](https://www.npmjs.com/), run `npm install` on the root folder; this will install the cypress CLI module and other dependencies, which are the [faker](https://www.npmjs.com/package/faker) module and a cypress [plugin](https://github.com/Bkucera/cypress-plugin-tab) for pressing the tab key, along with [another plugin](https://github.com/flotwig/cypress-log-to-output) for capturing the browser console output. In case you already have cypress installed, it is better to avoid installing it again in this folder; for this, run the commands `npm install faker`, `npm install -D cypress-log-to-output` and `npm install -D cypress-plugin-tab` individually.
- Configure the desired parameters: The repository's root folder contains two JSON files which have the configuration parameters for each test. Open them and edit the parameters as needed. You can change the baseURL, the seed for the test, the percentage of events, the delay between events, and the number of events.
- Run the desired tester: The commands for running the tests must be executed from the root folder, so do not forget to change de directory again with the `cd` command. For the random tester, run `cypress run --config-file ./monkey-config.json`. For the slightly smarter random tester, run `cypress run --config-file ./smart-monkey-config.json`. 

\* Note: The default browser is Electron 78 in headless mode. In order to test another browser, add the `--browser <browser-name-or-path>` option to the run command, indicating which of the [supported browsers](https://docs.cypress.io/guides/guides/launching-browsers.html#Browsers) you want to use

## The testers
Cypress is an E2E test runner built over JavaScript. We used this technology due to the facility for managing web pages in a variety of browsers including Chrome, Canary, Edge, Electron, etc. and the record-and-replay functionality. The idea of the first tester is to perform a completely random test on a web application, inspired on a similar tester, the [Android Monkey](https://developer.android.com/studio/test/monkey). The second tester exists due to the high rate of errors and low probability of getting events that change the application's state of the Monkey tester.

## Events
After evaluating a series of possible events, we defined the following 8 categories in which the events could be grouped by:
- **Random Click Events**:
Left, Right or Double clicks performed to an element from a random position
- **Scroll Events**:
Scrolling the page up, down, to the left or to the right.
- **Selector Focus Events**:
Focusing on elements from a random position, considering their HTML tags. The equivalent for pressing tab into a focusable element
- **Keypress Events**:
Introducing a character inside of a focused element. The equivalent for pressing a key from the keyboard when focusing an element.
- **Special Keypress Events**:
Typing special characters inside of a focused element. The special keys include Enter, Supr, Esc, Backspace, Arrows, and possible modifiers such as Shift, Alt or Ctrl.
- **Page Navigation Events**:
Typical navigation that an user could perform, go to the last page or to the next page in the navigation Stack.
- **Browser Chaotic Events**:
Events that change the browser configuration such as changing the viewport, clearing local storage or clearing the cookies.
- **Selector Click Events**:
Clicks performed to a specific type of element considering the HTML tags that typically induce an interaction such as `<a>`, `<button>`, `<input type="submit">`; also, events of filling and clearing an input element.

## Run
Luego de comprender el detalle de los eventos que genera esta versión de Monkey, puede cambiar los archivos de configuración según su necesidad y posteriormente ejecutar la prueba. En particular, es necesario que asegure que el atributo ‘baseURL' corresponda con https://www.google.com/. Para ejecutar la prueba abra una terminal y ubíquese en el directorio raíz del repositorio. Desde allí, descargue las dependencias del proyecto ejecutando el comando:
- `npm install`

Esto instalará un directorio llamado "node_modules", que contiene las librerías que se utilizan como parte del código del proyecto. El comando puede tardar un poco en completarse, dado que instala librerías de gran tamaño. En caso de que usted cuente con alguna de las dependencias mencionadas en el apartado "Herramientas utilizadas", puede optar por instalar las otras dependencias de forma manual para reducir el tamaño de los archivos descargados, siguiendo las instrucciones del archivo README.md.

Luego de este paso, puede ejecutar Cypress por medio del comando:

- `cypress run -C <archivo-config>`

- Ejemplo: `cypress run -C monkey-config.json`

En el siguiente paso se explicará lo que sucede al ejecutar la prueba.

Es necesario que indique el archivo de configuración correspondiente a la versión que quiere utilizar (monkey-config.json o smart-monkey-config.json). Otros flags que funcionan pueden ser los siguientes:

- `-b <browser>` : permite elegir el navegador en que se va a correr la prueba. Los posibles valores de browser incluyen chrome, chromium, edge, electron, firefox. En caso de no incluir esta opción, Cypress buscará un navegador adecuado.
- `--headed` : permite ejecutar la prueba en modo headed, lo que quiere decir que ejecuta el navegador como un programa con interfaz en la máquina.
- `--headless` : permite ejecutar la prueba en modo headless, lo que quiere decir que el navegador no se ejecuta como un programa con interfaz en la máquina.
- `-port <num-puerto>` : permite configurar otro puerto diferente al puerto por defecto para correr la prueba.

## Results and report
En la misma carpeta "results" mencionada anteriormente, podrá ver un archivo en formato .html, que contiene un reporte indicando los eventos que se indujeron en la aplicación web y su resultado. Abra el reporte en un navegador, y podrá ver una sección inicial con el nombre de la aplicación que se va a probar, la fecha de la ejecución y la semilla utilizada, como se muestra a continuación:
