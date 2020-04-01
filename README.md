# **Explicación del ejercicio:**



*   Se necesita tener una funcionalidad a nivel de negocio, que permita al cliente de la aplicación bancaria gft wallet poder recargar tiempo aire a su celular.

Fase desde no se tiene nada hecho en la app:



*   Inicio desde el cliente selecciona de todas sus cuentas, cual quiere utilizar para hacer el retiro de la misma para la recarga.
*   El cliente debe seleccionar cual telefónica tiene como proveedor
*   El cliente debe seleccionar el monto y moneda de la recarga

Despues se le va a mostrar una pantalla de confirmación para decirle al cliente, como quedaría la operación que va a realizar:


## **Datos:**



*   cuenta seleccionada
*   telefónica seleccionada
*   monto y moneda de la recarga seleccionada
*   fecha de operación
*   número de celular del cliente

Al final habrá un botón que confirmara la recarga y al tener éxito en ella, se le devolverá los mismos datos al cliente agregando el folio de operación para que el banco pueda rastrear dicha operación, si el cliente tuvo algún problema.


## **¿Que se les pide?**



1. Diagrama uml bien hecho: nombre de campos de atributos en camel case, nombre de entidades o clases en upper camel case, tipo de cada campo y tipo de relación que tienen entre entidades o recursos
2. Número de servicios que se deben de diseñar y aplicar para que se contemple toda la funcionalidad de negocio antes descrita, que hará cada servicio y que se le va enviar de entrada y salida


### **Entidades:**



*   Cliente
    *   id # integer
    *   nombreCompleto #String
    *   dirección #String
    *   rfc #String
    *   -> telefono #agregacion
    *   -> cuenta #agregacion
    *   _public_ Cuentas[] verCuentas ( )
    *   _public_ boolean agregarTelefono ( )
    *   _public_ boolean agregarCuenta ( )
*   Telefono
    *   id # integer
    *   numero #String
    *   claveLada #String
    *   -> compañiaTelefonica # composicion
*   Cuenta
    *   id # integer
    *   -> operacion # agregacion
*   Cuenta Bancaria &lt;- Cuenta
    *   clabe # String
    *   _public_ boolean realizarCargo ( )
    *   -> banco # composicion
*   Banco
    *   id # integer
    *   nombre #String
*   Cuenta Debito &lt;- Cuenta Bancaria
    *   saldo # double
*   Cuenta Credito &lt;- Cuenta Bancaria
    *   limiteCredito # double
*   Compañia telefonica
    *   id # integer
    *   nombre # String
    *   _public_ boolean realizarRecarga ( )
*   Operacion
    *   id # integer
    *   fecha # date
    *   status # String
*   Recarga &lt;- Operacion
    *   monto # double
    *   moneda # String
    *   _public_ boolean ejecutarSolicitud ( )
    *   ->telefono # composicion
    *   ->cuentaBancaria # composicion


### 


### **Recursos**



*   Recurso: Banco
    *   URI: /Banco/
        *   Verbo: GET
        *   Regresa: List&lt;Bancos>
*   Recurso: Telefonica
    *   URI: /Telefonica/
        *   Verbo: GET
        *   Regresa: List&lt;Telefonica>
*   Recurso: Cuenta
    *   URI: /Cliente/{cliente}/Cuenta/
        *   verbo: POST
        *   Parametros: banco={banco}&clabe={clabe}
        *   Regresa: 201, Cuenta
    *   URI: /Cliente/{cliente}/Cuenta/{cuenta}/
        *   verbo: GET
        *   Regresa: 200, Cuenta
    *   URI: /Cliente/{cliente}/Cuenta/
        *   verbo: GET
        *   Regresa: 200, List[Cuenta]
*   Recurso: Telefono
    *   URI: /Cliente/{cliente}/Telefono/
        *   verbo: POST
        *   Parametros: numero={numero}&telefonica={telefonica}
        *   Regresa: 201, Telefono
    *   URI: /Cliente/{cliente}/Telefono/
        *   Verbo: GET
        *   Regresa: 200, List&lt;Telefono>
    *   URI: /Cliente/{cliente}/Telefono/{telefono}/
        *   Verbo: GET
        *   Regresa: 200, Telefono
*   Recurso: Recarga
    *   URI: /Cliente/{cliente}/Recarga/{operacion}
        *   verbo: GET
        *   Regresa: 200, Recarga
    *   URI: /Cliente/{cliente}/Recarga
        *   verbo: GET
        *   Regresa: 200, List[Recarga]
    *   URI: /Cliente/{cliente}/Recarga/
        *   Verbo: POST
        *   Parametros: cuenta={Cuenta},monto={monto},moneda={moneda},telefono={Telefono}
        *   Regresa: 201, Recarga


### **Diagramas**

![Diagrama de clases](https://raw.githubusercontent.com/agustincperalta/APIWalletRecargas/master/diagrama.png)

*   Cliente
*   Operacion, Recarga
*   Telefono, Telefonica, Banco
*   Cuenta, Cuenta Bancaria, Debito, Credito
