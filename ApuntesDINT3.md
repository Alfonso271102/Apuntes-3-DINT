# Comandos

```cs
publc RelayCommand SiguienteCommand { get; } --> Definimos el command

public MainWindowVM(){
  SiguienteCommand = new RelayCommand(Avanzar); --> Instanciamos el command con el metodo que ejecuta
}

public void Avanzar(){
  Actual++
}
```
- Asociar al comando:
```xml
<Button Command="{Binding Path=SiguienteCommand}"></Button>
```

# Mas de una vista
1. Crear ventana hija (agregar -> ventana wpf)
2. Agregar una nueva clase que será su VM (como todos los VM hereda de ObservableObject)
3. Asociar VM con la ventana hija
```cs
private VentanaHijaVM vm;
public VentanaHija(){
    InicializeComponent();
    vm = new VentanaHijaVM();
    this.DataContext = vm;
}
```
4. Agregar el NavegationService.cs (class)
```cs
public AbrirVentanaHija()
{
  VentanaHija nueva = VentanaHija(); // Si queremos que no se abra una ventana cada vez, tendriamos que crear esta ventana como un campo de la clase
  nueva.show();
}
```
5. En el MainWindowVM
```cs
//creamos la referencia al servicio
private NavegationService servicio;

// Lo instanciamos en el constructor
public MainWindow()
{
  AbrirVentanaCommand = new RelayCommando(AbrirVentana);
  servicio = new NavigationService();

  private void AbrirVentana()
  {
    servicio.AbrirVentanaHija();
  }
}
```
# Diálogos (ventana hija con modificaciones)
1. No mostrar con .show, sino con .showDialog
2. La ventana retorna un bool -> se puede controlar con DialogResult (boton aceptar -> retorna DialogResult = true)
3. Se debe de poner el isdefault = true (este boton necesita manejador de eventos, no puede ser command, normalmente, dentro de este metodo, se pone DialogResult = true (antes de esto sae pueden ejecutar otras acciones)) e iscancel=true (en dos borones)
4. Propiedades a poner en propiedades de window:
```xml
  ShowInTaskbar="False"
  ResizeMode="NoResize"
```

# Aplicaciones monoventa
- Click derecho agregar -> Control de usuario
- MainWindow -> tendrá un:
 ```xml
--> Decidimos en cada momento que contenido se carga
<ContentControl
	Content="{Binding Path= ContenidoOpccion}"> -> Lo podemos cambiar con un boton con un command por ejemplo
 </ContentControl>
//En vm tendriamos que definir la propiedad private UserControl contenidoVista;
 ```
 Con el servicio navegacion instanciamos la pantalla -> tendra métodos que cargen los contenidos en funcion de los metodos -> return new Opcion4UserControl();
 
  ```xml
 <TabControl>
	<TabItem>
	  <local:UserControl1></UserControl> -> caragaria al momento todas las vistas  
	</TabItem>
 </TabControl>
 ```

# Mensajeria



























