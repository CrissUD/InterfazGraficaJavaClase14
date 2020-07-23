# Interfaz Gráfica en Java

Curso propuesto por el grupo de trabajo Semana de Ingenio y Diseño (**SID**) de la Universidad Distrital Francisco Jose de Caldas.

## Monitor

**Cristian Felipe Patiño Cáceres** - Estudiante de Ingeniería de Sistemas de la Universidad Distrital Francisco Jose de Caldas

# Clase 14

## Objetivos

* Reconocer la forma de utilizar el servicio Gráficos avanzados para realizar decoraciones especiales en los objetos gráficos dentro de nuestro proyecto.
* Determinar el proceso interno de cada uno de los métodos contenidos en del servicio Gráficos avanzados reconociendo cual es propósito de cada uno de ellos.
* Identificar que elementos gráficos intervienen para cumplir con las acciones de cada uno de los métodos contenidos en el servicio Gráficos avanzados.
* Mostrar ejemplos adicionales para brindar una mayor explicación de ciertas particularidades contenidas en algunos de los métodos.

# Antes de Comenzar

Recordando un poco nuestro recorrido en la sesión anterior implementamos el uso de **Canvas** y entre otras cosas aprendimos como **pintar figuras (strings, rectángulos, lineas, arcos, óvalos, polígonos e imágenes)**. Vimos un ejemplo del uso de **Areas para hacer acciones como combinación o sustracción con estas**, finalmente utilizamos los eventos del Mouse para **pintar un rectángulo en tiempo real**.

<div align='center'>
    <img  src='https://i.imgur.com/X4m3u07.png'>
    <p>Pintando figuras sobre el Canvas</p>
</div>

<div align='center'>
    <img  src='https://i.imgur.com/Xdls9LS.png'>
    <p>Simulación de bordes redondeados con uso de Areas.</p>
</div>

<div align='center'>
    <img  src='./gifs/Canvas1.gif'>
    <p>Dibujando rectángulos usando Mouse Events.</p>
</div>

### **Aclaración:**

En esta sesión se mencionara mucho la palabra **Component** pero en esta ocasión no nos estaremos refiriendo a componentes gráficos o a la clase **Component** de algún componente. **Component** es también una clase en Java de la cual heredan todos los objetos gráficos que hemos manipulado, como los botones, labels, textField etc. Es valida la aclaración entonces por que al coincidir el nombre puede confundir un poco, sin embargo cuando se hable de la palabrá **Component** en esta sesión hablaremos de esta clase particular de Java, a menos que se nombre explícitamente algún componente gráfico que hemos creado antes.

# Servicio Gráficos Avanzados

En esta sesión vamos a explicar cada uno de los métodos contenidos en este servicio, para explorar este servicio se verán los siguientes items:

* **Decoración de una Tabla**.
* **Personalización de un SrollBar**.
* **Creación de Bordes Difuminados**.
* **Creación de Bordes Redondeados**.
* **Creación de Bordes Circulares**.

# Decoración de una Tabla

En la sesión 11 vimos brevemente que podíamos decorar nuestra tabla usando nuestro nuevo servicio **GraficosAvanzadosService**, esto nos dio la posibilidad de intercalar el color de las filas de la tabla, cambiar el color de fuente, escoger el tipo de fuente, personalizar la cabecera e incluso proporcionar un color en caso de seleccionar alguna de las filas. 

<div align='center'>
    <img  src='https://i.imgur.com/K8JYhqm.png'>
    <p>Tabla personalizada.</p>
</div>

Sin embargo se explico poco o nada de como se lograron todas estas cosas. Para empezar el método que se uso para personalizar la tabla fue **setDefaultRenderer()** este puede recibir por parámetro:
* **ColumnClass**: Debe recibir una clase que representa las columnas que tendrá la tabla, este parámetro por lo general no representa una vital importancia ya que no influye en la personalización y por esto se suele colocar como argumento **Object.class** representando que se enviara una clase cualquiera.
* **TableCellRenderer**: Es una interfaz que contiene ciertos métodos dispuesto para la personalización de una tabla.

***Nota:** El parámetro ColumnClass solo es necesario para el objeto JTable, para el JTableHeader solo se pide el segundo parámetro.*

<div align='center'>
    <img  src='https://i.imgur.com/PeyXnBy.png'>
    <p>Método para personalizar las tablas.</p>
</div>

Lo primero que vamos a ver es la definición del método del servicio **GraficosAvanzadosService** que nos ayuda con la personalización de la tabla.
```javascript
public DefaultTableCellRenderer devolverTablaPersonalizada(
        Color colorPrincipal, Color colorSecundario, Color colorSeleccion, Color colorFuente, Font fuente
){
    ...
    ...
}
```

Podemos observar lo siguiente: 
* El método retorna un objeto de tipo **DefaultTableCellRender** este objeto cumple un papel crucial ya que esta clase es la que implementa a la interfaz **TableCellRenderer**, otra particularidad importante es que este objeto se puede tratar como un **JLabel**, si entramos al código Java podemos confirmar esto.
<div align='center'>
    <img  src='https://i.imgur.com/BYu3AoZ.png'>
    <p>Clase de Java que ya implementa la interfaz que necesitamos y hereda de un JLabel.</p>
</div>

* El método recibe por parámetro:
    * **colorPrincipal**: En nuestro caso el color principal representa el color de fondo de las filas impares.
    * **colorSecundario**: En nuestro caso el color secundario representa el color de fondo de las filas pares.
    * **colorSeleccion**: En nuestro caso el color de selección representa el color de fondo que tendrá una fila una vez se seleccione a traves de un click con el mouse.
    * **colorFuente:** Representa el color de fuente que tendrá toda la tabla.
    * **Fuente:** Representa la fuente que tendrá el contenido de toda la tabla.

***Nota:** Cabe aclarar que se recalca la frase **en nuestro caso** ya que mas adelante nos podemos dar cuenta que podemos personalizar una tabla de varias maneras y esta solo es una de ellas.*

Como ya hemos visto a lo largo del curso para poder obtener **interfaces** es necesario una clase que la implemente, como es el caso de los eventos, la clase que implementa las interfaces de los eventos cuando hablamos de un componente gráfico es la clase **Component** y a traves de esta, la clase **Template** puede indicarle a sus objetos gráficos que podrán escuchar esos eventos. Este es un caso igual, para poder obtener el parámetro/interfaz **TableCellRenderer** debemos usar una clase que implemente a esta interfaz y retornar un objeto de dicha clase. Como acabamos de ver la clase de Java **DefaultTableCellRender** cumple con este criterio asi que vamos a crear una **ejemplificación anónima** de esta clase y de una vez vamos a indicarle al método que vamos a retornar este objeto anónimo que acabamos de ejemplificar.

```javascript
public DefaultTableCellRenderer devolverTablaPersonalizada(
        Color colorPrincipal, Color colorSecundario, Color colorSeleccion, Color colorFuente, Font fuente
){
    return new DefaultTableCellRenderer();
}
```

Hasta el momento nuestro código está bien y no nos notifica ningún error, sin embargo queremos hacer unas configuraciónes sobre este objeto, es por eso que una vez terminan los paréntesis de la ejemplificación y antes del punto y coma vamos a abrir unas llaves **"{}"** para realizar una configuración adicional:
```javascript
devolverTablaPersonalizada(
        Color colorPrincipal, Color colorSecundario, Color colorSeleccion, Color colorFuente, Font fuente
){
    return new DefaultTableCellRenderer(){

    };
}
```

Para los JDK 10 en adelante el compilador va a sugerir crear un identificador de la clase, de hecho en el código se han venido creando seriales en las clases para hacer caso a esta sugerencia, este serial lo realiza el propio compilador cuando se observa la sugerencia y no es mas que un atributo de tipo **long**, así que esta al ser una clase anónima lo pide de igual forma como una sugerencia, esto no es obligatorio solo es una pequeña recomendación del compilador:
```javascript
public DefaultTableCellRenderer devolverTablaPersonalizada(
    Color colorPrincipal, Color colorSecundario, Color colorSeleccion, Color colorFuente, Font fuente
){
    return new DefaultTableCellRenderer(){
        private static final long serialVersionUID = -8946942932242371111L;
    };
}
```

Ahora para realizar la personalización de la tabla debemos implementar un método de la interfaz **TableCellRenderer**, este método es **getTableCellRendererComponent** recordemos que para denotar que estamos implementando un método desde una interfaz es necesario colocar el decorador **@Override** o de lo contrario Java interpretará ese método como cualquier otro que hayamos creado y no funcionará como esperamos. 

```javascript
public DefaultTableCellRenderer devolverTablaPersonalizada(
    Color colorPrincipal, Color colorSecundario, Color colorSeleccion, Color colorFuente, Font fuente
){
    return new DefaultTableCellRenderer(){
        private static final long serialVersionUID = -8946942932242371111L;

        @Override
        public Component getTableCellRendererComponent(
            JTable table, Object value, boolean isSelected, boolean hasFocus, int row, int column
        ){
            
        }
    };
}
```

Este método retorna un tipo de objeto **Component** pero debemos aclarar de una vez que en realidad lo que estamos retornando aquí es cada una de las celdas que tiene la tabla. Este método entonces se encarga de tomar las celdas dentro de la tabla una por una y tratar cada celda como si fuera un **JLabel** para que nosotros podamos personalizar dicha celda como queramos.

Ademas este método recibe varios parámetros como:
* **JTable: tabla**: Nos indica la tabla donde esta contenida la celda que vamos a personalizar.
* **Object: value**: Nos indica el contenido que tiene dicha celda (el texto en nuestro caso, cabe aclarar que una celda puede contener una imágen un botón un textfield etc).
* **boolean isSelected**: Nos sirve para comprobar si la fila donde esta la celda dentro de la tabla se ha seleccionado.
* **boolean hasFocus**: Nos sirve para verificar si la celda en particular se seleccionó.
* **int row**: Nos indica la fila donde la celda esta posicionada.
* **int column**: Nos indica la columna donde la celda esa seleccionada.

***Nota:** Como este método se esta implementando desde una interfaz estos parámetros los pasa automáticamente  el compilador, nosotros no debemos preocuparnos por pasar estos datos, un caso similar ocurre con los eventos, donde los parámetros **ActionEvent**, **MouseEvent** etc, son pasados a traves del compilador y nosotros hacemos uso de estos sin necesidad de pasar este parámetro de forma manual. También ocurre con el objeto **Graphics** del canvas. Esto se cumple siempre y cuando se utilice el decorador **@Override** de lo contrario el compilador no sabrá que este es un método implementado y nos pedirá enviar estos parámetros de forma manual.*


En este punto el compilador nos esta sacando un error ya que el método no esta retornando nada, bueno para esto vamos a crear un JLabel que representara la celda y será el objeto que retornemos:
```javascript
public DefaultTableCellRenderer devolverTablaPersonalizada(
    Color colorPrincipal, Color colorSecundario, Color colorSeleccion, Color colorFuente, Font fuente
){
    return new DefaultTableCellRenderer(){
        private static final long serialVersionUID = -8946942932242371111L;

        @Override
        public Component getTableCellRendererComponent(
            JTable table, Object value, boolean isSelected, boolean hasFocus, int row, int column
        ){
            JLabel celda;

            return celda;
        }
    };
}
```

Debemos ejemplificar el JLabel pero para indicar que este JLabel es la celda actual en la tabla vamos a tener que obtener la celda a traves de una **llamada recursiva** al mismo método pero esta vez a traves del objeto **super**, esto denota que la interfaz misma será la encargada de darnos la celda actual, como se llamará al mismo método le debemos pasar como argumentos los parámetros que recibimos. Ademas como explicamos el método **getTableCellRendererComponent** nos retorna un objeto tipo **Component** y para tratarlo como JLabel debemos hacer un **Cast de objeto**.

```javascript
public DefaultTableCellRenderer devolverTablaPersonalizada(
    Color colorPrincipal, Color colorSecundario, Color colorSeleccion, Color colorFuente, Font fuente
){
    return new DefaultTableCellRenderer(){
        private static final long serialVersionUID = -8946942932242371111L;

        @Override
        public Component getTableCellRendererComponent(
            JTable table, Object value, boolean isSelected, boolean hasFocus, int row, int column
        ){
            JLabel celda = (JLabel) super.getTableCellRendererComponent (table, value, isSelected, hasFocus, row, column);

            return celda;
        }
    };
}
```

Cabe aclarar que este paso no es obligatorio, podemos trabajar la celda a traves de la palabra clave **this**, pero esto querrá decir que vamos a tratar la celda como un tipo de objeto **Component** y no como un **JLabel**, las dos formas son compatibles, al fin y al cabo un **JLabel** hereda de un **Component**. Sin embargo tratar a la celda como un **JLabel** nos da mas posibilidades, por ejemplo cambiar el color o la fuente de la letra no se podría realizar si trabajamos la celda como un **Component**.

Con esto ya tenemos nuestra celda en forma de Label y podemos manipularla: 
* Queremos que nuestros label tengan color de fondo, estos por defecto son transparente asi que para indicarle que si tendrá color llamarémos al método **setOpaque** y le pasaremos un true.
* Vamos a indicar que el label tendrá la fuente que pasamos como parámetro.
* Vamos a indicar que el color de la letra del label sera la que pasamos como parámetro.
* Ademas para nuestro caso vamos a indicar que el contenido del JLabel lo queremos de forma centrada.
```javascript
public DefaultTableCellRenderer devolverTablaPersonalizada(
    Color colorPrincipal, Color colorSecundario, Color colorSeleccion, Color colorFuente, Font fuente
){
    return new DefaultTableCellRenderer(){
        private static final long serialVersionUID = -8946942932242371111L;

        @Override
        public Component getTableCellRendererComponent(
            JTable table, Object value, boolean isSelected, boolean hasFocus, int row, int column
        ){
            JLabel celda = (JLabel) super.getTableCellRendererComponent (table, value, isSelected, hasFocus, row, column);
            celda.setOpaque(true);
            celda.setFont(fuente);
            celda.setForeground(colorFuente);
            celda.setHorizontalAlignment(SwingConstants.CENTER);
            return celda;
        }
    };
}
```

Por el momento no hemos realizado ninguna restricción, esto quiere decir que todas las celdas de la tabla van a cumplir con el hecho de tener **color de fondo, tener la fuente  y el color de fuente que le pasamos y ademas estar centradas**. Ahora queremos empezar a realizar restricciones para personalizar la tabla como queremos y aquí viene la aclaración y es que a traves de estas restricciones el desarrollador podrá personalizar la tabla a su antojo, en nuestro caso lo haremos de cierta forma pero se sabe de antemano que se podría realizar de otras maneras.

Nosotros queremos que las filas dentro de nuestra tabla tengan un color de fondo intercalado, es decir que si las filas impares tendrán cierto color, las pares otro. Para eso podemos tomar el parámetro que nos indica en que fila esta nuestra celda y preguntar si es una fila par o impar, esto se hace con el **modulo** que en caso de devolvernos  un 0 se sabe que es par, de lo contrario será impar:
```javascript
public DefaultTableCellRenderer devolverTablaPersonalizada(
    Color colorPrincipal, Color colorSecundario, Color colorSeleccion, Color colorFuente, Font fuente
){
    return new DefaultTableCellRenderer(){
        private static final long serialVersionUID = -8946942932242371111L;

        @Override
        public Component getTableCellRendererComponent(
            JTable table, Object value, boolean isSelected, boolean hasFocus, int row, int column
        ){
            JLabel celda = (JLabel) super.getTableCellRendererComponent (table, value, isSelected, hasFocus, row, column);
            celda.setOpaque(true);
            celda.setFont(fuente);
            celda.setForeground(colorFuente);
            celda.setHorizontalAlignment(SwingConstants.CENTER);
            if (row % 2 != 0)
                // Configuración filas impares
            else
                // Configuración filas pares
            return celda;
        }
    };
}
```

Ahora solo basta con configurar el color de fondo de la celda por cada condición:
```javascript
public DefaultTableCellRenderer devolverTablaPersonalizada(
    Color colorPrincipal, Color colorSecundario, Color colorSeleccion, Color colorFuente, Font fuente
){
    return new DefaultTableCellRenderer(){
        private static final long serialVersionUID = -8946942932242371111L;

        @Override
        public Component getTableCellRendererComponent(
            JTable table, Object value, boolean isSelected, boolean hasFocus, int row, int column
        ){
            JLabel celda = (JLabel) super.getTableCellRendererComponent (table, value, isSelected, hasFocus, row, column);
            celda.setOpaque(true);
            celda.setFont(fuente);
            celda.setForeground(colorFuente);
            celda.setHorizontalAlignment(SwingConstants.CENTER);
            if (row % 2 != 0)
                celda.setBackground(colorPrincipal);
            else
                celda.setBackground(colorSecundario);
            return celda;
        }
    };
}
```

Para finalizar con la personalización queremos que una vez se seleccióne una celda, cambie de color toda la fila donde esta se encuentra, para esto podemos tomar el parámetro **isSelected** que nos retornara un booleano el cual nos indicará si la fila donde está la celda se seleccionó, si se quisiera ser mas especifico y solo se quisiera cambiar el color de fondo de esa única celda en ese caso utilizaríamos el parámetro **hasfocus**.
```javascript
public DefaultTableCellRenderer devolverTablaPersonalizada(
    Color colorPrincipal, Color colorSecundario, Color colorSeleccion, Color colorFuente, Font fuente
){
    return new DefaultTableCellRenderer(){
        private static final long serialVersionUID = -8946942932242371111L;

        @Override
        public Component getTableCellRendererComponent(
            JTable table, Object value, boolean isSelected, boolean hasFocus, int row, int column
        ){
            JLabel celda = (JLabel) super.getTableCellRendererComponent (table, value, isSelected, hasFocus, row, column);
            celda.setOpaque(true);
            celda.setFont(fuente);
            celda.setForeground(colorFuente);
            celda.setHorizontalAlignment(SwingConstants.CENTER);
            if (row % 2 != 0)
                celda.setBackground(colorPrincipal);
            else
                celda.setBackground(colorSecundario);
            if(isSelected){
            }
            return celda;
        }
    };
}
```
Dentro de este condicional haremos dos cosas, primero cambiaremos el color de fondo de la fila, luego cambiaremos el color de fuente, y esto debido a que suponemos que en la mayoría de los casos cuando se seleccione una fila se querrá mostrar un color fuerte que resalte, asi que esto podría hacer que la letra dentro de la celda se opaque un poco y para evitar esto cambiaremos el color de fuente a blanco para que la letra pueda resaltar aun mas.

```javascript
public DefaultTableCellRenderer devolverTablaPersonalizada(
    Color colorPrincipal, Color colorSecundario, Color colorSeleccion, Color colorFuente, Font fuente
){
    return new DefaultTableCellRenderer(){
        private static final long serialVersionUID = -8946942932242371111L;

        @Override
        public Component getTableCellRendererComponent(
            JTable table, Object value, boolean isSelected, boolean hasFocus, int row, int column
        ){
            JLabel celda = (JLabel) super.getTableCellRendererComponent (table, value, isSelected, hasFocus, row, column);
            celda.setOpaque(true);
            celda.setFont(fuente);
            celda.setForeground(colorFuente);
            celda.setHorizontalAlignment(SwingConstants.CENTER);
            if (row % 2 != 0)
                celda.setBackground(colorPrincipal);
            else
                celda.setBackground(colorSecundario);
            if(isSelected){
                celda.setBackground(colorSeleccion);
                celda.setForeground(Color.WHITE);
            }
            return celda;
        }
    };
}
```

De esta forma ha quedado listo nuestro método para personalizar la tabla.

# Personalización de un SrollBar

Cuando creamos la tabla en la sesión 11 también se realizo la personalización del ScrollBar vertical del **JScrollPane** esto debido a que el ScrollBar que viene por defecto se ve algo antiguo y no concuerda muchas veces con el resto de nuestra interfaz, para personalizar este objeto usamos el método **getVerticalScrollBar** de nuestro **JScrollPane** que nos devolvía el objeto del **ScrollBar** vertical y seguido a eso llamamos al método **setUI** este es el encargado de configurar una personalización al ScrollBar.

<div align='center'>
    <img  src='https://i.imgur.com/GGtu7Pi.png'>
    <p>Uso de métodos para personalizar el ScrollBar vertical.</p>
</div>

El método **SetUI** debe recibir por parámetro un objeto de tipo **ScrollBarUI**, este objeto será el responsable de la personalización del ScrollBar.

Antes de continuar debemos ver las partes que conforman un **ScrollBar** y de esta forma comprenderemos mejor el código que se explicará a continuación:
<div align='center'>
    <img  src='https://i.imgur.com/MZaNSYw.png'>
    <p>Partes de un ScrollBar.</p>
</div>

Podemos observar que un ScrollBar contiene 3 partes principales: 
* **Track:** Es el recuadro de fondo que contiene los demás elementos y por el cual podrá moverse el Thumb.
* **Thumb:** Es el recuadro o barra que se moverá a traves del Track y por el cual nosotros podremos navegar en la pantalla.
* **Buttons:** Son los botones que están en cada esquina del track y con los cuales también podremos navegar y mover el Thumb.

Notamos que para obtener este ScrollBar personalizado llamamos al método **devolverScrollPersonalizado** del servicio **GraficosAvanzadosService**. vamos a ver que realizamos en este método, para empezar veamos su definición:
```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    ...
    ...
}
```

Podemos notar que este método retorna un objeto de tipo **BasicScrollBarUI** y podemos verificar que este objeto es compatible con un **ScrollBarUI** ya que el primero mencionado hereda de este ultimo, podemos verificarlo si entramos a la definición de esta clase:

<div align='center'>
    <img  src='https://i.imgur.com/WgyRj2d.png'>
    <p>Definición de la clase BasicScrollBarUI.</p>
</div>

También podemos notar que el método recibe por parámetros varias cosas:
* **Grosor**: Representa el grosor de la barra de navegación dentro del ScrollBar (Thumb).
* **Radio**: Representa el radio de los bordes de la barra de navegación (Thumb) Para hacer que esta sea un rectángulo con bordes redondeados o un rectángulo recto.
* **ColorFondo**: Representa el color del recuadro donde se encuentra la barra (color del track).
* **ColorBarraNormal**: Representa el color de la barra mientras esta quieta.
* **ColorBarraArrastrada**: Representa el color de la barra mientras se esta oprimiendo con el Mouse y se arrastra.

Como definimos que el método retorna un objeto de este tipo vamos a crear un objeto a traves de una ejemplificación anónima de esta clase y de una vez vamos a indicar que retornaremos este objeto anónimo:

```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    return new BasicScrollBarUI();
}
```

Nuevamente como queremos una personalización de este objeto vamos a abrir corchetes después de los paréntesis de la ejemplificación:
```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    return new BasicScrollBarUI(){
        
    };
}
```

Para personalizar completamente nuestro ScrollBar debemos implementar algunos métodos de su clase padre para asi poder decorar cada parte:
```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    return new BasicScrollBarUI(){
        @Override
        protected JButton createDecreaseButton(int orientation) {
        }
    
        @Override
        protected JButton createIncreaseButton(int orientation) {
        }
    
        @Override
        protected void paintTrack(Graphics g, JComponent c, Rectangle r) {

        }
    
        @Override
        protected void paintThumb(Graphics g, JComponent c, Rectangle r) {
        }
    };
}
```

* Los dos primeros métodos **createDecreaseButton** representan la personalización de ambos botones del ScrollBar.
* El método **paintTrack** se encarga de la personalización del track o recuadro de fondo del ScrollBar.
* El método **paintThumb** se encarga de la personalización del Thumb o barra de navegación del ScrollBar.

Vamos a empezar con la configuración de los botones, el método **createDecreaseButton** nos exige retornar un botón asi que crearemos un botón para luego retornarlo.

```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    return new BasicScrollBarUI(){
        @Override
        protected JButton createDecreaseButton(int orientation) {
            JButton boton = new JButton();
            return boton;
        }
    
        @Override
        protected JButton createIncreaseButton(int orientation) {
            JButton boton = new JButton();
            return boton;
        }
    
        ...
        ...
    };
}
```

Con los botónes podemos crearlos a nuestro antojo, podemos incluso llamar a nuestro otro servicio **sObjGraficosService** para construirlos. 

Otra posibilidad es no crear ningún botón es decir que no vamos a manejar estos métodos y podemos borrarlos de nuestro código, en este caso se generarán unos botónes que Java trae por defecto:

<div align='center'>
    <img  src='https://i.imgur.com/65hIs7p.png'>
    <p>ScrollBar con botones por defecto.</p>
</div>

También se puede retornar un botón como lo estamos haciendo en este momento es decir solo ejemplificarlo y luego retornarlo, esto hará que se creen dos botones vacíos pero con su funcionamiento correcto.

<div align='center'>
    <img  src='https://i.imgur.com/0UD2CqG.png'>
    <p>ScrollBar con botones vacíos.</p>
</div>

En nuestro caso queremos que en nuestro ScrollBar los botónes no sean visibles, para esto podríamos indicarle a nuestros botónes que tengan un tamaño de 0 en x y 0 en y llamando al método **setSize**, sin embargo esto no funcionará, el compilador volverá a crear un botón vació como en la anterior imágen. En este caso vamos a necesitar el método **setPreferredSize** que nos pide como parámetro un objeto dimensión, primero vamos a crear una variable de tipo dimensión dentro de la configuración del objeto **BasicScrollBar** :

```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    return new BasicScrollBarUI(){
        private Dimension d = new Dimension();
        ...
        ...
    }
}
```

Al ejemplificar el objeto dimensión y dejar el constructor vacío () se esta especificando que esta dimensión no ocupara ningún espacio, ahora le vamos a dar esta dimensión a nuestros botones:

```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    return new BasicScrollBarUI(){
        @Override
        protected JButton createDecreaseButton(int orientation) {
            JButton boton = new JButton();
            boton.setPreferredSize(d);
            return boton;
        }
    
        @Override
        protected JButton createIncreaseButton(int orientation) {
            JButton boton = new JButton();
            boton.setPreferredSize(d);
            return boton;
        }

        ...
        ...
    };
}
```

De esta forma nuestros botones no serán visibles dentro del ScrollBar. Ahora vamos a ocuparnos del **track** para este caso vamos a pintar un rectángulo que ocupara el total de las dimensiones del ScrollBar, y se pintara con el color de fondo que se proporcionó por parámetros:
```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    return new BasicScrollBarUI(){
        ...
        ...
    
        @Override
        protected void paintTrack(Graphics g, JComponent c, Rectangle r) {
            g.setColor(colorFondo);
            g.fillRect(r.x, r.y, r.width, r.height);
        }
    
        ...
        ...
    };
}
```

Para pintar el rectángulo usamos el parámetro **Graphics** que tiene el método implementado, para hallar las dimensiones del ScrollBar como la posición y el tamaño usamos el objeto **Rectangle**.

Es hora de pintar el **Thumb** o barra de navegación, en este caso queremos pintar un rectángulo con bordes redondeados, como el rectángulo tendrá curvas, sería bueno pintarlo con un objeto **Graphics2D** asi que vamos a crear este objeto a traves del padre **Graphics** que obtenemos desde los parámetros, de una vez configuraremos los algoritmos para una mejor calidad de renderizado:

```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    return new BasicScrollBarUI(){
        ...
        ...
    
        @Override
        protected void paintThumb(Graphics g, JComponent c, Rectangle r) {
            Graphics2D g2 = (Graphics2D) g.create();
            g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            g2.setRenderingHint(RenderingHints.KEY_STROKE_CONTROL, RenderingHints.VALUE_STROKE_NORMALIZE);
        }
    };
}
```

Crearemos ahora un objeto tipo **JScrollBar** esto para verificar algunas condiciones, podemos obtenerlo a traves del parámetro **Component** y vamos a hacer el **Cast** correspondiente:
```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    return new BasicScrollBarUI(){
        ...
        ...
    
        @Override
        protected void paintThumb(Graphics g, JComponent c, Rectangle r) {
            Graphics2D g2 = (Graphics2D) g.create();
            g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            g2.setRenderingHint(RenderingHints.KEY_STROKE_CONTROL, RenderingHints.VALUE_STROKE_NORMALIZE);
            JScrollBar sb = (JScrollBar) c;
        }
    };
}
```
Ahora vamos a crear una condición y es que en los casos en que un objeto gráfico no ocupe un tamaño mayor a las dimensiones del **JScrollPane** no necesitamos mostrar los **ScrollBarr**, esto lo haremos preguntando si el ScrollBar esta habilitado o no, en caso de estar deshabilitado no retornaremos nada:
```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    return new BasicScrollBarUI(){
        ...
        ...
    
        @Override
        protected void paintThumb(Graphics g, JComponent c, Rectangle r) {
            Graphics2D g2 = (Graphics2D) g.create();
            g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            g2.setRenderingHint(RenderingHints.KEY_STROKE_CONTROL, RenderingHints.VALUE_STROKE_NORMALIZE);
            JScrollBar sb = (JScrollBar) c;
            if (!sb.isEnabled())
                return;
        }
    };
}
```

Ahora en el caso en que si este habilitado vamos a crear una segunda condición, preguntando si el usuario esta arrastrando la barra a traves del mouse, en ese caso vamos a configurar el color cuando se esta arrastrando que pasamos por el parámetro:
```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    return new BasicScrollBarUI(){
        ...
        ...
    
        @Override
        protected void paintThumb(Graphics g, JComponent c, Rectangle r) {
            Graphics2D g2 = (Graphics2D) g.create();
            g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            g2.setRenderingHint(RenderingHints.KEY_STROKE_CONTROL, RenderingHints.VALUE_STROKE_NORMALIZE);
            JScrollBar sb = (JScrollBar) c;
            if (!sb.isEnabled())
                return;
            else if (isDragging)
                g2.setPaint(colorBarraArrastrada);
        }
    };
}
```
Crearemos una tercera condición, donde vamos a preguntar si el usuario esta moviendo el ScrollBar a traves del Wheel o rueda del Mouse, para este caso nosotros optamos configurarle el color normal de la barra pasado por parámetro pero el desarrollador podrá elegir si dejar este color o cambiarlo por otro:
```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    return new BasicScrollBarUI(){
        ...
        ...
    
        @Override
        protected void paintThumb(Graphics g, JComponent c, Rectangle r) {
            Graphics2D g2 = (Graphics2D) g.create();
            g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            g2.setRenderingHint(RenderingHints.KEY_STROKE_CONTROL, RenderingHints.VALUE_STROKE_NORMALIZE);
            JScrollBar sb = (JScrollBar) c;
            if (!sb.isEnabled())
                return;
            else if (isDragging)
                g2.setPaint(colorBarraArrastrada);
            else if (isThumbRollover())
                g2.setPaint(colorBarraNormal);
        }
    };
}
```
Finalmente para el caso por defecto (Cuando la barra esta habilitada) pero no se esta moviendo vamos a configurar el color de la barra normal recibido por parámetro:
```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    return new BasicScrollBarUI(){
        ...
        ...
    
        @Override
        protected void paintThumb(Graphics g, JComponent c, Rectangle r) {
            Graphics2D g2 = (Graphics2D) g.create();
            g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            g2.setRenderingHint(RenderingHints.KEY_STROKE_CONTROL, RenderingHints.VALUE_STROKE_NORMALIZE);
            JScrollBar sb = (JScrollBar) c;
            if (!sb.isEnabled())
                return;
            else if (isDragging)
                g2.setPaint(colorBarraArrastrada);
            else if (isThumbRollover())
                g2.setPaint(colorBarraNormal);
            else
                g2.setPaint(colorBarraNormal);
        }
    };
}
```

Ahora se crea un condicional aparte, este será para preguntar si se va a pintar un **ScrollBar Horizontal o Vertical**, esto es importante ya que en muchos casos se podrían usar cualquiera de los dos y debemos tener presente esto, para saber esto basta con tomar las dimensiones del ScrollBar y preguntar cual dimensión es mas grande, el ancho o el alto:
```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    return new BasicScrollBarUI(){
        ...
        ...
    
        @Override
        protected void paintThumb(Graphics g, JComponent c, Rectangle r) {
            Graphics2D g2 = (Graphics2D) g.create();
            g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            g2.setRenderingHint(RenderingHints.KEY_STROKE_CONTROL, RenderingHints.VALUE_STROKE_NORMALIZE);
            JScrollBar sb = (JScrollBar) c;
            if (!sb.isEnabled())
                return;
            else if (isDragging)
                g2.setPaint(colorBarraArrastrada);
            else if (isThumbRollover())
                g2.setPaint(colorBarraNormal);
            else
                g2.setPaint(colorBarraNormal);
            
            if(r.width < r.height)
                //ScrollBar Vertical
            else
                //ScrollBar Horizontal
        }
    };
}
```
Ahora vamos a pintar el **Rectángulo con bordes redondeados**.
```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    return new BasicScrollBarUI(){
        ...
        ...
    
        @Override
        protected void paintThumb(Graphics g, JComponent c, Rectangle r) {
            Graphics2D g2 = (Graphics2D) g.create();
            g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            g2.setRenderingHint(RenderingHints.KEY_STROKE_CONTROL, RenderingHints.VALUE_STROKE_NORMALIZE);
            JScrollBar sb = (JScrollBar) c;
            if (!sb.isEnabled())
                return;
            else if (isDragging)
                g2.setPaint(colorBarraArrastrada);
            else if (isThumbRollover())
                g2.setPaint(colorBarraNormal);
            else
                g2.setPaint(colorBarraNormal);
            
            if(r.width < r.height)
                g2.fillRoundRect();
            else
                g2.fillRoundRect();
        }
    };
}
```
recordemos que para dibujar este tipo de rectángulos debemos pasar como argumento la posición, el tamaño del recuadro y el tamaño de los bordes redondeados. Para ambos casos queremos que nuestro **Thumb** quede en el medio para esto vamos a realizar la operación de restar las mitades entre el grosor del **Track** y el **Thumb** como hemos explorado con anterioridad:
```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    return new BasicScrollBarUI(){
        ...
        ...
    
        @Override
        protected void paintThumb(Graphics g, JComponent c, Rectangle r) {
            Graphics2D g2 = (Graphics2D) g.create();
            g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            g2.setRenderingHint(RenderingHints.KEY_STROKE_CONTROL, RenderingHints.VALUE_STROKE_NORMALIZE);
            JScrollBar sb = (JScrollBar) c;
            if (!sb.isEnabled())
                return;
            else if (isDragging)
                g2.setPaint(colorBarraArrastrada);
            else if (isThumbRollover())
                g2.setPaint(colorBarraNormal);
            else
                g2.setPaint(colorBarraNormal);
            
            if(r.width < r.height)
                g2.fillRoundRect((r.width - grosor) / 2, r.y);
            else
                g2.fillRoundRect(r.x, (r.height - grosor) / 2);
        }
    };
}
```
Para el primer caso al ser vertical restaremos la mitad de los anchos, mientras que en el segundo caso al ser horizontal restaremos la mitad de los altos. Ahora vamos a configurar el tamaño del **Thumb**:
```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    return new BasicScrollBarUI(){
        ...
        ...
    
        @Override
        protected void paintThumb(Graphics g, JComponent c, Rectangle r) {
            Graphics2D g2 = (Graphics2D) g.create();
            g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            g2.setRenderingHint(RenderingHints.KEY_STROKE_CONTROL, RenderingHints.VALUE_STROKE_NORMALIZE);
            JScrollBar sb = (JScrollBar) c;
            if (!sb.isEnabled())
                return;
            else if (isDragging)
                g2.setPaint(colorBarraArrastrada);
            else if (isThumbRollover())
                g2.setPaint(colorBarraNormal);
            else
                g2.setPaint(colorBarraNormal);
            
            if(r.width < r.height)
                g2.fillRoundRect((r.width - grosor) / 2, r.y, grosor, r.height);
            else
                g2.fillRoundRect(r.x, (r.height - grosor) / 2, r.width, grosor);
        }
    };
}
```

Para el primer caso al ser un **ScrollBar Vertical** se dejara un ancho igual al grosor proporcionado por parámetro y la altura que por defecto se da para el Thumb, para el segundo caso al ser un **ScrollBar Horizontal** se dejara un ancho por defecto que se da para el Thumb y la altura igual al grosor que se proporciono por parámetro. Esto hará que las barras de navegación sean tan delgadas o gruesas como el desarrollador elija.

Finalmente vamos a configurar los bordes, para este caso se proporciona el radio que se paso por parámetro, de esta forma la barra podrá quedar con bordes redondeados o como un rectángulo con esquinas rectas, depende de como configure el desarrollador.
```javascript
public BasicScrollBarUI devolverScrollPersonalizado(
    int grosor, int radio, Color colorFondo, Color colorBarraNormal, Color colorBarraArrastrada
){
    return new BasicScrollBarUI(){
        ...
        ...
    
        @Override
        protected void paintThumb(Graphics g, JComponent c, Rectangle r) {
            Graphics2D g2 = (Graphics2D) g.create();
            g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            g2.setRenderingHint(RenderingHints.KEY_STROKE_CONTROL, RenderingHints.VALUE_STROKE_NORMALIZE);
            JScrollBar sb = (JScrollBar) c;
            if (!sb.isEnabled())
                return;
            else if (isDragging)
                g2.setPaint(colorBarraArrastrada);
            else if (isThumbRollover())
                g2.setPaint(colorBarraNormal);
            else
                g2.setPaint(colorBarraNormal);
            
            if(r.width < r.height)
                g2.fillRoundRect((r.width - grosor) / 2, r.y, grosor, r.height, radio, radio);
            else
                g2.fillRoundRect(r.x, (r.height - grosor) / 2, r.width, grosor, radio, radio);
        }
    };
}
```

Para el caso de la tabla no se personalizo el ScrollBar Horizontal ya que las columnas no ocupabán mas del ancho del panel, sin embargo en dado caso también podría realizarse. A continuación se muestra un ejemplo del uso de los dos ScrollBar en una interfaz de ejemplo:

<div align='center'>
    <img  src='https://i.imgur.com/1s4v2DX.png'>
    <p>Ejemplo de la personalización de ScrollBar Vertical y Horizontal</p>
</div>

# Creación de Bordes Difuminados.

Vamos a ver un ejemplo de la creación de bordes difuminados, este método es solo un prototipo y por el momento solo funciona para algunos casos especiales, funciona perfectamente con colores grises claros (a partir de 210 de color) u otros colores muy claros también y que el fondo sea blanco. Aun asi se puede proporcionar cualquier color y no habrá ningún error, sin embargo no se vera tan bien el efecto Para realizar esta técnica nos vamos a basar el 3 cosas importantes:

* Creación de bordes lineales a través del borde tipo **LineBorder**.
* Creación de bordes combinados (union entre dos bordes) de forma acumulada a través del borde **CompoundBorder**.
* Aumento de color en las tres lineas (Rojo, Verde, Azul) a traves de la descomposición del color.

Primero vamos a ver la definición del método:
```javascript
public Border devolverBordeDifuminado(Color colorBase, int grosor){
}
```
Podemos notar que el método retorna un objeto tipo **Border** y recibe como parámetros:
* **ColorBase**: Es el color con el que inicia el borde y al cual se va a difuminar.
* **Grosor**: Es un entero que representa que tan grueso se quiere construir el borde, este por lo general no debe tener mucho grosor.

A continuación vamos a crear un borde que será el borde final y el cual vamos a retornar: 
```javascript
public Border devolverBordeDifuminado(Color colorBase, int grosor){
    Border bordeFinal = null;
    return bordeFinal;
}
```

Vamos a crear a continuación el borde inicial, este tendrá el color base y será un borde Lineal:
```javascript
public Border devolverBordeDifuminado(Color colorBase, int grosor){
    Border bordeFinal = null;
    Border bordeInicial =  BorderFactory.createLineBorder(colorBase, 1, true);
    return bordeFinal;
}
```

Ahora vamos a crear un nuevo color que será derivado del color base, este tendrá las mismas coordenadas de color pero aumentada con 5 unidades. Para esto debemos descomponer el color base en sus 3 lineas principales (RGB) esto se puede realizar tomando al color en cuestión y llamando sus métodos **getRed(), getGreen(), getBlue()**:
```javascript
public Border devolverBordeDifuminado(Color colorBase, int grosor){
    Border bordeFinal = null;
    Border bordeInicial =  BorderFactory.createLineBorder(colorBase, 1, true);  
    Color siguienteColor = new Color(colorBase.getRed() + 5, colorBase.getGreen() + 5, colorBase.getBlue() + 5);
    return bordeFinal;
}
```
Ahora vamos a crear una variable que nos servirá como contador y será clave para determinar el grosor del borde.
```javascript
public Border devolverBordeDifuminado(Color colorBase, int grosor){
    Border bordeFinal = null;
    Border bordeInicial =  BorderFactory.createLineBorder(colorBase, 1, true);  
    Color siguienteColor = new Color(colorBase.getRed() + 5, colorBase.getGreen() + 5, colorBase.getBlue() + 5);
    int contador = 0;
    return bordeFinal;
}
```
A partir de aquí vamos a iterar sobre un ciclo, primero vamos a crear la condición para que el ciclo pueda seguir iterando, para empezar el máximo valor posible cuando se habla de colores es 255, y como notaron vamos a ir aumentando el color de 5 en 5, esto quiere decir que si en algún punto el color en cualquiera de sus 3 lineas (RGB) supera el valor de 200, ya no podrá entrar mas al ciclo, de los contrario se le va a sumar 5 y esto nos dará un valor superior a 255 y generará un error. Por otro lado debemos verificar que el borde no pase del grosor dado por parámetro.
```javascript
public Border devolverBordeDifuminado(Color colorBase, int grosor){
    Border bordeFinal = null;
    Border bordeInicial =  BorderFactory.createLineBorder(colorBase, 1, true);  
    Color siguienteColor = new Color(colorBase.getRed() + 5, colorBase.getGreen() + 5, colorBase.getBlue() + 5);
    int contador = 0;
    while(
        siguienteColor.getRed() < 251 && siguienteColor.getGreen() < 251 && 
        siguienteColor.getBlue() < 251 && contador < grosor
    ){
    }
    return bordeFinal;
}
```
Ahora bien si estas condiciones son cumplidas vamos a empezar a construir nuestro borde compuesto, para empezar debemos construir la siguiente parte del borde compuesto, este será otro borde lineal pero esta vez tendrá el siguiente color (que es un poco mas claro) es decir que será el borde externo:
```javascript
public Border devolverBordeDifuminado(Color colorBase, int grosor){
    Border bordeFinal = null;
    Border bordeInicial =  BorderFactory.createLineBorder(colorBase, 1, true);  
    Color siguienteColor = new Color(colorBase.getRed() + 5, colorBase.getGreen() + 5, colorBase.getBlue() + 5);
    int contador = 0;
    while(
        siguienteColor.getRed() < 251 && siguienteColor.getGreen() < 251 && 
        siguienteColor.getBlue() < 251 && contador < grosor
    ){
        Border bordeExterno =  BorderFactory.createLineBorder(siguienteColor, 1, true);
    }
    return bordeFinal;
}
```
Ahora podemos realizar un borde Compuesto y recordando un poco la **Clase 3** de nuestro curso, un borde compuesto se compone por 2 bordes asi que como parámetros recibe 2 bordes: **El borde externo como primer parámetro y el El borde interno como segundo parámetro**, para realizar el borde compuesto debemos crear una condición y esto es debido a que la primera vez que se pase por el ciclo el borde compuesto estará conformado por **el borde externo y el borde inicial**. Pero después de esto como el borde ya tendrá dos bordes integrados el borde se conformará por **el borde externo y así mismo**, de esta forma podemos acumular varios bordes en uno solo:
```javascript
public Border devolverBordeDifuminado(Color colorBase, int grosor){
    Border bordeFinal = null;
    Border bordeInicial =  BorderFactory.createLineBorder(colorBase, 1, true);  
    Color siguienteColor = new Color(colorBase.getRed() + 5, colorBase.getGreen() + 5, colorBase.getBlue() + 5);
    int contador = 0;
    while(
        siguienteColor.getRed() < 251 && siguienteColor.getGreen() < 251 && 
        siguienteColor.getBlue() < 251 && contador < grosor
    ){
        Border bordeExterno =  BorderFactory.createLineBorder(siguienteColor, 1, true);
        if(contador == 0)
                bordeFinal = BorderFactory.createCompoundBorder(bordeExterno, bordeInicial);
            else
                bordeFinal = BorderFactory.createCompoundBorder(bordeExterno, bordeFinal);
    }
    return bordeFinal;
}
```
Por ultimo vamos a tener que actualizar el **Siguiente Color** y el **Contador**, con el siguiente color vamos a sumarle 5 unidades al color actual (sumarle a si mismo) y con el contador sumaremos una unidad nada mas:
```javascript
public Border devolverBordeDifuminado(Color colorBase, int grosor){
    Border bordeFinal = null;
    Border bordeInicial =  BorderFactory.createLineBorder(colorBase, 1, true);  
    Color siguienteColor = new Color(colorBase.getRed() + 5, colorBase.getGreen() + 5, colorBase.getBlue() + 5);
    int contador = 0;
    while(
        siguienteColor.getRed() < 251 && siguienteColor.getGreen() < 251 && 
        siguienteColor.getBlue() < 251 && contador < grosor
    ){
        Border bordeExterno =  BorderFactory.createLineBorder(siguienteColor, 1, true);
        if(contador == 0)
            bordeFinal = BorderFactory.createCompoundBorder(bordeExterno, bordeInicial);
        else
            bordeFinal = BorderFactory.createCompoundBorder(bordeExterno, bordeFinal);
        siguienteColor = new Color(
            siguienteColor.getRed() + 5, siguienteColor.getGreen() + 5, siguienteColor.getBlue() + 5
        );
        contador ++;
    }
    return bordeFinal;
}
```
Nuestro método esta listo para usarse, vamos a usarlo a traves del otro servicio **RecursosService** para tener el borde guardado y dispuesto para las partes de nuestro proyecto que lo requieran. En nuestro Servicio **RecursosService** vamos a declarar una referencia hacia el otro servicio y luego lo vamos a obtener:
* **Declaración:**
```javascript
// Dentro del servicio RecursosService
private GraficosAvanzadosService sGraficosAvanzados;
```
* **Obtención del servicio:**
```javascript
// Dentro del constructor
sGraficosAvanzados = GraficosAvanzadosService.getService();
```
Ahora vamos a declarar un borde llamado **bordeDifuminado** y lo crearemos con ayuda de nuestro servicio **GraficosAvanzadosService:**
* **Declaración:**
```javascript
private Border bordeDifuminado;
```
* **Ejemplificación:**
```javascript
// Dentro del constructor
devolverBordeDifuminado(new Color(215, 215, 215), 8);
```
* **Método get**:
```javascript
public Border getBordeDifuminado(){
    return bordeDifuminado;
}
```
Es hora de usar nuestro borde, para este caso vamos a usarlos en nuestro componente **Accion** cambiando el borde gris que tenía por el nuevo borde gris difuminado:
```javascript
// Dentro del constructor de la clase AccionTemplate
this.setBorder(sRecursos.getBordeDifuminado());
```
Vamos a realizar unos pequeños ajustes de posicionamiento bajando 10px en el eje Y de la imágen, título y párrafo:
<div align='center'>
    <img  src='https://i.imgur.com/4QGkMKR.png'>
    <p>Ajuste de posiciones</p>
</div>

Nuestro borde difuminado se ve así:
<div align='center'>
    <img  src='https://i.imgur.com/KLfZEQU.png'>
    <p>Implementación de bordes difuminados.</p>
</div>

# Creación de Bordes Redondeados

Como hemos comprobado antes, no es posible que alguno de nuestros objetos gráficos tengan un borde redondeados, en la clase anterior a traves del canvas realizamos una simulación de como podríamos crear un borde de este estilo, es hora de implementarlo. Primero vamos a ver la definición del método:
```javascript
public Border DibujarBordeRedondeado (Color color, int radio, boolean esLineal, Image imagen) {
}
```
Podemos observar que el método retorna un objeto tipo Border y recibe por parámetros:
* **Color de borde:** Muchas veces se va querer construir este tipo de bordes con un contorno de algún color, para estos casos enviaremos un color.
* **Radio:** Representa el ancho y alto que tendrán los bordes redondeados del rectángulo, entre mas alto mas se notarán estos bordes.
* **esLineal**: Es un booleano que nos sirve para verificar si queremos que solo se vea el contorno del borde o vamos a crear un borde redondeado sin una linea que denote el borde.
* **Imágen**: Este parámetro se utilizara en casos especiales en donde el objeto gráfico al cual se le va a aplicar el borde redondeado está encima de una imágen o fondo.

Con lo anterior podemos darnos cuenta que existen 3 casos para querer usar estos bordes:
* Borde redondeado con un contorno (una linea que denota el borde).
* Borde redondeado sin contorno.
* Borde redondeado para un elemento que esta encima de una imagén de fondo.

Para el proyecto se usara el segundo caso pero se mostrarán ejemplos de los otros dos casos para que se entienda el propósito. Lo primero que vamos a hacer es crear un objeto tipo **Border** y retornarlo ya que es lo que nos exige el método:
```javascript
public Border DibujarBordeRedondeado (Color color, int radio, boolean esLineal, Image imagen) {
    Border bordeRedondeado = new Border();
    return bordeRedondeado;
}
```

Ahora seguramente el compilador nos arroja un error y es que un **Border** en realidad es una interfaz y al ser de este tipo nos va a exigir que implementemos ciertos métodos que trae por defecto:
```javascript
public Border DibujarBordeRedondeado (Color color, int radio, boolean esLineal, Image imagen) {
    Border bordeRedondeado = new Border(){

        @Override
        public void paintBorder(Component c, Graphics g, int x, int y, int width, int height) {
        }

        @Override
        public Insets getBorderInsets(Component c) {
            return null;
        }

        @Override
        public boolean isBorderOpaque() {
            return false;
        }  
    };
    return bordeRedondeado;
}
```

Vamos a empezar con los dos últimos métodos ya que son los mas cortos, un borde exige crear un **insert** o **Padding** esto significa un espacio entre el borde y el contenido del objeto gráfico, para esto vamos a crear un objeto tipo **Inserts** que exige en su constructor 4 parámetros estos son 4 enteros que representan:
* **Espacio entre borde superior y contenido.**
* **Espacio entre borde derecho y contenido.**
* **Espacio entre borde inferior y contenido.**
* **Espacio entre borde izquierdo y contenido.**
Para hacerlo general vamos a crear un Padding pequeño de 2px dentro del método **getBorderInserts**, por otro lado con el método **isBorderOpaque** vamos a retornar un **true** para habilitar los casos en que se dibujará el contorno del borde y en caso de no, nosotros lo gestionaremos:
```javascript
public Border DibujarBordeRedondeado (Color color, int radio, boolean esLineal, Image imagen) {
    Border bordeRedondeado = new Border(){
        ...

        @Override
        public Insets getBorderInsets(Component c) {
            return new Insets(2, 2, 2, 2);
        }

        @Override
        public boolean isBorderOpaque() {
            return true;
        }
    };
    return bordeRedondeado;
}
```

Ahora nos concentraremos unicamente en el método **paintBorder**, pueden notar que recibe como parámetros:
* **Componente**: Objeto Gráfico al que se le añadirá el borde.
* **Graphics**: Objeto con el cual se pintará el borde redondeado.
* **Coordenadas:** Las coordenadas donde esta el objeto gráfico al cual se le añadirá el borde redondeado.
* **Tamaño:** El tamaño del objeto gráfico al cual se le añadirá el borde redondeado.

Recordemos que al ser un método implementado estos parámetros no los pasa el compilador de forma automática. También podemos cambiar el nombre de la variable y no habrá ningún problema, en este caso cambiaremos los dos últimos al español.

Como vamos a pintar un borde con curvas vamos a necesitar crear un objeto **Graphics2D** y de una vez implementar los algoritmos de calidad de renderizado:
```javascript
public Border DibujarBordeRedondeado (Color color, int radio, boolean esLineal, Image imagen) {
    Border bordeRedondeado = new Border(){

        @Override
        public void paintBorder(Component c, Graphics g, int x, int y, int ancho, int alto) {
            Graphics2D g2= (Graphics2D) g;
            g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            g2.setRenderingHint(RenderingHints.KEY_STROKE_CONTROL, RenderingHints.VALUE_STROKE_NORMALIZE);
        }

        ...
    };
    return bordeRedondeado;
}
```

En la clase anterior vimos que para crear un borde necesitábamos el uso de **Areas** ya que necesitamos realizar operaciónes de sustracción y ademas no queremos tapar el contenido del objeto gráfico que tenga este borde, vamos a declarar el area principal, por otro lado necesitamos obtener el **objeto gráfico padre** esto quiere decir el objeto gráfico que lo contiene, por ejemplo un botón puede estar contenido dentro de un panel, este ultimo será entonces el padre del botón, y necesitamos obtener al padre para obtener su color de fondo y asi pintar las esquinas sobrantes del borde de dicho color. Esto se hace con el método **getParent**.
```javascript
public Border DibujarBordeRedondeado (Color color, int radio, boolean esLineal, Image imagen) {
    Border bordeRedondeado = new Border(){

        @Override
        public void paintBorder(Component c, Graphics g, int x, int y, int ancho, int alto) {
            Graphics2D g2= (Graphics2D) g;
            g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            g2.setRenderingHint(RenderingHints.KEY_STROKE_CONTROL, RenderingHints.VALUE_STROKE_NORMALIZE);
            Area area;
            Component padreContenedor  = c.getParent();
        }

        ...
    };
    return bordeRedondeado;
}
```
Vamos a crear nuestro rectángulo redondeado como un **objeto gráfico 2D** y le pasaremos sus dimensiónes de una vez con ayuda de los parámetros recibidos.
```javascript
public Border DibujarBordeRedondeado (Color color, int radio, boolean esLineal, Image imagen) {
    Border bordeRedondeado = new Border(){

        @Override
        public void paintBorder(Component c, Graphics g, int x, int y, int ancho, int alto) {
            Graphics2D g2= (Graphics2D) g;
            g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            g2.setRenderingHint(RenderingHints.KEY_STROKE_CONTROL, RenderingHints.VALUE_STROKE_NORMALIZE);
            Area area;
            Component padreContenedor  = c.getParent();
            RoundRectangle2D rectanguloBordeado = new RoundRectangle2D.Double();
            rectanguloBordeado.setRoundRect(x, y, ancho - 1, alto - 1, radio, radio);
        }

        ...
    };
    return bordeRedondeado;
}
```
Noten que el ancho y alto se deja con un pixel menos esto para que se pueda ver el contorno en caso de que el usuario quiera mostrarlo, por otro lado el radio de los bordes lo obtenemos de los parámetros globales del método **DibujarBordeRedondeado**.
Ahora vamos a realizar una condicional que es quizás la parte mas importante del método, aquí se preguntará si el borde que se quiere dibujar será lineal o por el contrario sera un borde sin contorno:
```javascript
public Border DibujarBordeRedondeado (Color color, int radio, boolean esLineal, Image imagen) {
    Border bordeRedondeado = new Border(){

        @Override
        public void paintBorder(Component c, Graphics g, int x, int y, int ancho, int alto) {
            Graphics2D g2= (Graphics2D) g;
            g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            g2.setRenderingHint(RenderingHints.KEY_STROKE_CONTROL, RenderingHints.VALUE_STROKE_NORMALIZE);
            Area area;
            Component padreContenedor  = c.getParent();
            RoundRectangle2D rectanguloBordeado = new RoundRectangle2D.Double();
            rectanguloBordeado.setRoundRect(x, y, ancho - 1, alto - 1, radio, radio);
            if(esLineal){
            }
            else{
            }
        }

        ...
    };
    return bordeRedondeado;
}
```
Esto se hace principalmente por que si se quiere dibujar un borde con contorno primero se tendrá que dibujar el fondo que se usa para borrar las partes sobrantes del borde y luego si pintar dicho borde, de lo contrario el fondo no dejara ver la linea del borde. 

Por otro lado si se quiere dibujar un borde sin contorno se tendrá que primero dibujar el borde y luego dibujar el fondo o de lo contrario el fondo va a tapar el contenido del objeto gráfico. Nótese que como vamos a dibujar sobre **Contextos** el orden de las cosas tiene una gran importancia para cada caso.

Para el caso que es lineal entonces vamos a llamar a dos métodos auxiliares con su respectivo orden **dibujarFondo** y **dibujarBorde**, estos métodos se explicaran en breve, por ahora es bueno notar que el método **DibujarBorde** retorna un Area y la vamos a igualara a la que nosotros declaramos. Para el caso de pintar un borde sin contorno se va a llamar con un orden contrario los dos métodos:

```javascript
public Border DibujarBordeRedondeado (Color color, int radio, boolean esLineal, Image imagen) {
    Border bordeRedondeado = new Border(){

        @Override
        public void paintBorder(Component c, Graphics g, int x, int y, int ancho, int alto) {
            Graphics2D g2= (Graphics2D) g;
            g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            g2.setRenderingHint(RenderingHints.KEY_STROKE_CONTROL, RenderingHints.VALUE_STROKE_NORMALIZE);
            Area area;
            Component padreContenedor  = c.getParent();
            RoundRectangle2D rectanguloBordeado = new RoundRectangle2D.Double();
            rectanguloBordeado.setRoundRect(x, y, ancho - 1, alto - 1, radio, radio);
            if(esLineal){
                dibujarFondo(c, padreContenedor, imagen, g2, ancho, alto);
                area = dibujarBorde(c, g2, color, x, y, ancho, alto, esLineal, rectanguloBordeado);
            }
            else{
                area = dibujarBorde(c, g2, color, x, y, ancho, alto, esLineal, rectanguloBordeado);
                dibujarFondo(c, padreContenedor, imagen, g2, ancho, alto);
            }
        }
        ...
    };
    return bordeRedondeado;
}
```
Finalmente para este método vamos a cambiar el contexto a nulo y pintar el area final, esto ultimo para evitar errores de pintado en futuros componentes y ademas para evitar el efecto pixeleado que se crea al poner un contexto distinto.
```javascript
public Border DibujarBordeRedondeado (Color color, int radio, boolean esLineal, Image imagen) {
    Border bordeRedondeado = new Border(){

        @Override
        public void paintBorder(Component c, Graphics g, int x, int y, int ancho, int alto) {
            Graphics2D g2= (Graphics2D) g;
            g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            g2.setRenderingHint(RenderingHints.KEY_STROKE_CONTROL, RenderingHints.VALUE_STROKE_NORMALIZE);
            Area area;
            Component padreContenedor  = c.getParent();
            RoundRectangle2D rectanguloBordeado = new RoundRectangle2D.Double();
            rectanguloBordeado.setRoundRect(x, y, ancho - 1, alto - 1, radio, radio);
            if(esLineal){
                dibujarFondo(c, padreContenedor, imagen, g2, ancho, alto);
                area = dibujarBorde(c, g2, color, x, y, ancho, alto, esLineal, rectanguloBordeado);
            }
            else{
                area = dibujarBorde(c, g2, color, x, y, ancho, alto, esLineal, rectanguloBordeado);
                dibujarFondo(c, padreContenedor, imagen, g2, ancho, alto);
            }
            g2.setClip(null);
            g2.draw(area);
        }
        ...
    };
    return bordeRedondeado;
}
```

Ahora vamos a explicar los dos métodos auxiliares que usamos, vamos a ver la definición del método **DibujarFondo**:
```javascript
public void dibujarFondo(Component c, Component padreContenedor, Image imagen, Graphics2D g2, int ancho, int alto){
}
```
Los parámetros que pide son:
* **Objeto Gráfico**: Al cual se le aplicará el borde.
* **Objeto Gráfico**: Que contiene al objeto que se le aplicará el borde.
* **Imágen**: En caso de que el objeto este encima de una imágen de fondo se pedirá esta.
* **Graphics2D**: El cual pintara el fondo.
* **Ancho y Alto**: Tamaño del Objeto Gráfico.

Lo primero que haremos es preguntar si se ha enviado una imágen, para ese caso se sabe que se tiene un fondo y se deberá pintar para simular una transparencia.
```javascript
public void dibujarFondo(Component c, Component padreContenedor, Image imagen, Graphics2D g2, int ancho, int alto){
    if(imagen != null)
        g2.drawImage(
            imagen, 
            0, 0, imagen.getWidth(null), imagen.getHeight(null),
            c.getX(), c.getY(), imagen.getWidth(null) + c.getX(), imagen.getHeight(null) + c.getY(),
            c
        );
    else{
    }
}
```
En este caso se dibuja una imágen usando el enfoque que se uso para pintar **Sprites**, lo que se hace es recortar la imágen original justo en la parte donde debería estar el objeto gráfico esto es para que en las esquinas que sobran del borde se vea pintada la imágen y de esa forma simule una transparencia. A continuación se muestra un ejemplo de lo que se quiere explicar con un Login.
<div align='center'>
    <img  src='https://i.imgur.com/PQUgadS.png'>
    <p>Bordes redondeados sin imágen.</p>
</div>

En este caso se quería implementar los bordes redondeados en el panel, sin embargo no se envió la imágen, incluso si se pintan los bordes restantes de transparente no hará efecto. 

<div align='center'>
    <img  src='https://i.imgur.com/R9xgzt6.png'>
    <p>Bordes redondeados con imágen.</p>
</div>
Para este caso se pinto la imágen justo en los bordes creando un efecto de transparencia. El método esta implementado de tal forma que el desarrollador no tiene que preocuparse mas que por enviar la imágen, eso si con las mismas dimensiónes que tiene la imágen en el fondo.

Volviendo con nuestro método, en caso contrarió cuando no hay una imágen de fondo se pintara simplemente un rectangulo que tendrá el color de fondo del contenedor padre.
```javascript
public void dibujarFondo(Component c, Component padreContenedor, Image imagen, Graphics2D g2, int ancho, int alto){
    if(imagen != null)
        g2.drawImage(
            imagen, 
            0, 0, imagen.getWidth(null), imagen.getHeight(null),
            c.getX(), c.getY(), imagen.getWidth(null) + c.getX(), imagen.getHeight(null) + c.getY(),
            c
        );
    else{
        g2.setColor(padreContenedor.getBackground());
        g2.fillRect(0, 0, ancho, alto);
    }
}
```
Ahora nos vamos a concentrar en el método **dibujarBorde**, primero veamos su definición:
```javascript
public Area dibujarBorde(
    Component c, Graphics2D g2, Color color, int x, int y, int ancho, int alto, boolean esLineal, RectangularShape figura
){
}
```
Este método retorna un objeto tipo **Area** y recibe por parámetros:
* **Objeto Gráfico**: Objeto que tendrá el borde redondeado.
* **Graphics 2D**: El objeto por el cual se pintará el borde.
* **Posición Objeto Gráfico**.
* **Tamaño Objeto Gráfico**.
* **Booleano**: Nos indica si el borde tendrá contorno o no.
* **Figura**: Recibe la figura que tendrá el borde ya que este método será llamado por varios otros métodos.

Lo primero que haremos es configurar el color del contorno del borde, en caso de ser nulo se pintara con el color del objeto gráfico para que no se vea, en caso contrario obtendrá el color que se paso por parámetro:
```javascript
public Area dibujarBorde(
    Component c, Graphics2D g2, Color color, int x, int y, int ancho, int alto, boolean esLineal, RectangularShape figura
){
    if(color == null)
        g2.setPaint(c.getBackground());
    else
        g2.setPaint(color);
}
```
Ahora vamos a crear el borde por medió de la operación entre areas, primero crearemos el area principal con la figura pasada por parámetro:
```javascript
public Area dibujarBorde(
    Component c, Graphics2D g2, Color color, int x, int y, int ancho, int alto, boolean esLineal, RectangularShape figura
){
    if(color == null)
        g2.setPaint(c.getBackground());
    else
        g2.setPaint(color);
    Area area = new Area(figura);
}
```
Ahora vamos a crear el area que representará los bordes sobrantes de la figura:
```javascript
public Area dibujarBorde(
    Component c, Graphics2D g2, Color color, int x, int y, int ancho, int alto, boolean esLineal, RectangularShape figura
){
    if(color == null)
        g2.setPaint(c.getBackground());
    else
        g2.setPaint(color);
    Area area = new Area(figura);
    Rectangle rectangulo = new Rectangle(0,0,ancho, alto);
    Area regionBorde = new Area(rectangulo);
}
```
Ahora realizaremos una **sustracción** entre areas para que el area **regionBorde** represente justamente las partes sobrantes del borde:
```javascript
public Area dibujarBorde(
    Component c, Graphics2D g2, Color color, int x, int y, int ancho, int alto, boolean esLineal, RectangularShape figura
){
    if(color == null)
        g2.setPaint(c.getBackground());
    else
        g2.setPaint(color);
    Area area = new Area(figura);
    Rectangle rectangulo = new Rectangle(0,0,ancho, alto);
    Area regionBorde = new Area(rectangulo);
    regionBorde.subtract(area);
}
```
Finalmente vamos a cambiar el contexto hacia esta area para que sea la única afectada cuando se pinte un fondo o en caso de que se haya pintado previamente el fondo, para que el contenido dentro del borde no sea tapado por el fondo, ademas vamos a retornar esta area para poder ser pintada en los métodos principales en que se llamen.
```javascript
public Area dibujarBorde(
    Component c, Graphics2D g2, Color color, int x, int y, int ancho, int alto, boolean esLineal, RectangularShape figura
){
    if(color == null)
        g2.setPaint(c.getBackground());
    else
        g2.setPaint(color);
    Area area = new Area(figura);
    Rectangle rectangulo = new Rectangle(0,0,ancho, alto);
    Area regionBorde = new Area(rectangulo);
    regionBorde.subtract(area);
    g2.setClip(regionBorde);
    return area;
}
```

Ya tenemos listo nuestro método para pintar bordes redondeados, vamos a crear un borde redondeado sin contorno desde nuestro servicio **sRecursos**:
* **Declaración:**
```javascript
// Dentro del servicio RecursosService
private Border bordeRedondeado;
```
* **Ejemplificación:**
```javascript
// Dentro del constructor
bordeRedondeado = sGraficosAvanzados.DibujarBordeRedondeado(null, 40, false, null);
```
* **Método get:**
```javascript
public Border getBordeRedondeado(){
    return bordeRedondeado;
}
```

Vamos a implementar este borde, en este caso vamos a incorporarlo en los botones **bEntrar y bRegistrar** de nuestro **Login**.

<div align='center'>
    <img  src='https://i.imgur.com/YD736hu.png'>
    <p>Incorporando el borde redondeado.</p>
</div>

nuestro login se ve así: 
<div align='center'>
    <img  src='https://i.imgur.com/tGnrLHK.png'>
    <p>Bordes redondeados incorporados.</p>
</div>

A continuación mostraremos otra versión de este mismo login donde se implementan **bordes redondeados con contorno** para el area de los JTextField.

<div align='center'>
    <img  src='https://i.imgur.com/HtD1wOM.png'>
    <p>Login de usuario con bordes redondeados con contorno incorporado.</p>
</div>

# Creación de Bordes Circulares

El caso de dibujar bordes circulares es bastante similar al anterior salvo algunas particularidades que explicaremos a continuación:
* **Definición del constructor**: En este caso se va a retornar un tipo de objeto **AbstractBorder** a diferencia del anterior donde devolvía un objeto tipo **Border**, este tipo de objetos actuá mejor para figuras diferentes a rectángulos. Como parámetros recibe:
    * **Color**: Color de contorno de la circunferencia.
    * **Boolean**: Nos indica si se quiere dibujar o no el contorno.
    * **Image**: Imágen en caso de que el objeto gráfico que incorporará el borde este encima de una imágen de fondo.

```javascript
public AbstractBorder DibujarBordeCircular(Color color, boolean esLineal, Image imagen) {
    ...
}
```

* **Tipo AbstractBorder**: Como vamos a retornar un tipo de objeto distinto este tiene otras particularidades, nos pedirá a modo de sugerencia un serial de clase, solo será necesario implementar el método **paintBorder**, los métodos **getBorderInsets e isBorderOpaque** ya no serán necesarios.
```javascript
public AbstractBorder DibujarBordeCircular(Color color, boolean esLineal, Image imagen) {
    AbstractBorder bordeCircular = new AbstractBorder() {
        private static final long serialVersionUID = 2009875951859777681L;

        @Override
        public void paintBorder(Component c, Graphics g, int x, int y, int ancho, int alto) {
            ...
            ...
        }
    };
    return bordeCircular;
}
```

* **Figura:** Dentro del método **paintBorder** el procedimiento realizado para crear el borde Redondeado va a ser exactamente el mismo a excepción de la figura que se creará, en este caso crearemos un elipse:
<div align='center'>
    <img  src='https://i.imgur.com/ptpouku.png'>
    <p>Creación de figura circular.</p>
</div>

Note que dentro de este método también se llaman los métodos **dibujarFondo y DibujarBorde**. De esta manera el método para dibujar bordes circulares esta listo para usarse.

Vamos a crear un borde circular sin contorno en nuestro servicio **sRecursos** para incorporarlo:
* **Declaración:**
```javascript
// Dentro del servicio RecursosService
private Border bordeCircular;
```

* **Ejemplificación:**
```javascript
// Dentro del constructor
bordeCircular = sGraficosAvanzados.DibujarBordeCircular(null, false, null);
```

* **Método get:**
```javascript
public Border getBordeCircular(){
    return bordeCircular;
}
```

Ahora podemos incorporar el borde circular, en este caso lo incorporaremos en la imágen del usuario que se encuentra en el componente gráfico **Navegación de usuario**.

<div align='center'>
    <img  src='https://i.imgur.com/HkZUz5B.png'>
    <p>Incorporando bode circular.</p>
</div>

Nuestra interfaz gráfica se ve así:
<div align='center'>
    <img  src='https://i.imgur.com/rJV3RFt.png'>
    <p>Borde Circular incorporado en nuestro proyecto.</p>
</div>

# Resultado

Si has llegado hasta aquí **!Felicidades!** ahora sabes como funcionan cada uno de los métodos del servicio **GraficosAvanzadosService** y entre todas las particularidades vistas aprendiste **Como decorar una tabla, como personalizar un ScrollBarr, como realizar bordes difuminados, bordes redondeados y bordes circulares.**. En la siguiente clase vamos a introducirnos en el posicionamiento gestionado por **LayoutsManager**.

# Actividad

Usa el Servicio **GraficosAvanzadosService** para personalizar de forma avanzada los objetos gráficos de tu proyecto, ademas como reto puedes crear un nuevo método que se encargue de la personalización de un **JComboBox**. En internet puedes encontrar varias formas de hacerlo pero procura mantenerlo bajo un método de este servicio.