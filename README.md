# Diagrama de secuencias
## Secuencias estereotipadas
- Sacar dinero

    ![Estereotipado de Sacar Dinero](EstereotipadoSacarDinero.png)

    @startuml
    
    actor Cliente
    
    boundary InterfazATM
    
    control ControlTransaccion
    
    entity BaseDatosCuentas
    
    Cliente -> InterfazATM : Seleccionar "Sacar dinero"
    
    InterfazATM -> ControlTransaccion : Iniciar transacción
    
    ControlTransaccion -> BaseDatosCuentas : Verificar saldo
    
    BaseDatosCuentas --> ControlTransaccion : Confirmar que hay saldo suficiente
    
    ControlTransaccion -> BaseDatosCuentas : Verificar limite diario
    
    BaseDatosCuentas --> ControlTransaccion : Confirmar que no supera el limite
    
    ControlTransaccion -> BaseDatosCuentas : Registrar retiro
    
    BaseDatosCuentas --> ControlTransaccion : Confirmar retiro
    
    ControlTransaccion --> InterfazATM : Notificar éxito
    
    InterfazATM --> Cliente : Entregar dinero
    
    @enduml
  
- Validarse

    ![Estereotipado de Validarse](EstereotipadoValidarse.png)
  
    @startuml
    
    actor Cliente
  
    boundary InterfazATM
    
    control ControlValidacion
    
    entity BaseDatosUsuarios
    
    Cliente -> InterfazATM : Introducir tarjeta y PIN
    
    InterfazATM -> ControlValidacion : Validar usuario
    
    ControlValidacion -> BaseDatosUsuarios : Verificar credenciales
    
    BaseDatosUsuarios --> ControlValidacion : Respuesta validación
    
    ControlValidacion --> InterfazATM : Resultado validación
    
    InterfazATM --> Cliente : Mostrar resultado
    
    @enduml

  ## Secuencia final

  - Sacar dinero

    ![Final de Sacar Dinero](FInalSacarDinero.png)

    @startuml
    
    actor Cliente
    
    boundary PantallaATM
    
    control GestorTransacciones
    
    entity RepositorioCuentas
    
    Cliente -> PantallaATM : Seleccionar "Sacar dinero"
    
    PantallaATM -> GestorTransacciones : Solicitar transacción
    
    GestorTransacciones -> RepositorioCuentas : Consultar saldo
    
    RepositorioCuentas --> GestorTransacciones : Respuesta saldo
    
    GestorTransacciones -> RepositorioCuentas : Verificar limite diario
    
    RepositorioCuentas --> GestorTransacciones : Confirmar que no supera el limite
    
    GestorTransacciones -> RepositorioCuentas : Registrar el retiro
    
    RepositorioCuentas --> GestorTransacciones : Confirmar el retiro
    
    GestorTransacciones -> RepositorioCuentas : Actualizar el historial de transacciones
    
    RepositorioCuentas --> GestorTransacciones : Confirmar la actualización de historial
    
    GestorTransacciones --> PantallaATM : Notificar del éxito
    
    PantallaATM --> Cliente : Entregar el dinero
    
    @enduml

  - Validarse
 
    ![Final de Validarse](FinalValidarse.png)
   
      @startuml
      
      actor Cliente
      
      boundary PantallaATM
      
      control GestorValidacion
      
      entity RepositorioUsuarios
      
      Cliente -> PantallaATM : Introducir tarjeta y PIN
      
      PantallaATM -> GestorValidacion : Enviar datos del usuario
      
      GestorValidacion -> RepositorioUsuarios : Consultar usuario
      
      RepositorioUsuarios --> GestorValidacion : Devolver datos usuario
      
      GestorValidacion -> RepositorioUsuarios : Registrar intento de acceso
      
      RepositorioUsuarios --> GestorValidacion : Confirmar registro de intento
      
      GestorValidacion --> PantallaATM : Confirmar validación
      
      PantallaATM --> Cliente : Mostrar mensaje validación
 
      @enduml
 
    ## Interpretacion del diagrama
 
    - El cliente introduce su tarjeta y el pin en la pantalla del ATM
    - Una vez introducido por pantalla se envian los datos al Gestor de validacion quien se encarga de controlar la validacion
    - El gestor consulta la informacion con el repositorio que guarda la informacion de los usuarios y recibe una respuesta del repositorio con los datos
    - Una vez que el control de validacion, valida el inicio de sesion le dice al repositorio que actualice el ultimo inicio de sesion del usuario y recibe la respuesta del repositorio una vez actualizado
    - Una vez realizado esto el gesto valida el inicio de sesion y la pantalla le muesta al usuario que ha iniciado sesion correctamente
   
    ## Respoder pregunta

    - ¿De que manera te ayuda un diagrama de secuencias durante el proceso de desarrollo del software?
   
    Ayuda a ver la interacciones que se van realizando a lo largo del proceso y quien lo realiza, ayudando a la hora de pasarlo a codigo al tener este boceto, ademas de ver los metodos que se usaran en el desarrollo
      
      
