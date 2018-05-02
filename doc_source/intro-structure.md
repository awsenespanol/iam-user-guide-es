# Entender cómo funciona IAM<a name="intro-structure"></a>

Antes de crear los usuarios, usted debe comprender cómo funciona IAM\. IAM proporciona la infraestructura necesaria para controlar la autenticación y la autorización para su cuenta. La infraestructura de IAM incluye los siguientes elementos:

**Temas**
+ [Principal](#intro-structure-principal)
+ [Solicitud](#intro-structure-request)
+ [Autenticación](#intro-structure-authentication)
+ [Autorización](#intro-structure-authorization)
+ [Acciones](#intro-structure-actions)
+ [Recursos](#intro-structure-resources)

![\[IntroToIAM_Diagram\]](http://docs.aws.amazon.com/IAM/latest/UserGuide/images/intro-diagram_800.png)

## Principal<a name="intro-structure-principal"></a>

Una entidad principal es una entidad que puede realizar una acción en un recurso de AWS\. Su usuario de IAM administrativo es su primera entidad principal\. Con el paso del tiempo, usted puede condecer a sus usuarios y los servicios asumir un rol\. Puede permitir a los usuarios federados o puede permitir el acceso mediante programación para que una aplicación pueda acceder a su cuenta de AWS. Los usuarios, los roles, los usuarios federados y las aplicaciones son todos entidades principales de AWS\.

## Solicitud<a name="intro-structure-request"></a>

Cuando una entidad principal intenta utilizar la Consola de administración de AWS, el API de AWS o la AWS CLI, la entidad principal envía una *solicitud* a AWS\. Una solicitud especifica la siguiente información:

+ Acciones \(u operaciones\) que la entidad principal desea realizar
+ Recursos sobre los cuales se realizan las acciones
+ Información principal, incluido el entorno desde el cual se realizó la solicitud

La información de solicitud se prepara a partir de diversas fuentes:

+ La entidad principal \(el solicitante\), que se determina en función a los datos de autorización\. Esto incluye los permisos agregados que están asociados con dicha entidad principal\.
+ Los datos de entorno, como la dirección IP, el agente del usuario, el estado de SSL habilitado, la hora del día\. Esta información se determina a partir de la solicitud\.
+ Los datos de recursos o los datos relacionados con el recurso que se está solicitando\. Esto puede incluir información como, por ejemplo, un nombre de una tabla de DynamoDB o una etiqueta de una instancia Amazon EC2\. Esta información se determina a partir de la solicitud\.

AWS permite recopilar esta información en un *contexto de solicitudes*, que se utiliza para evaluar y autorizar la solicitud\.

## Autenticación<a name="intro-structure-authentication"></a>

Como entidad principal, usted debe estar autenticado \(haber iniciado sesión en AWS\) para enviar una solicitud a AWS. También hay unos cuantos servicios, como Amazon S3, que permiten solicitudes de usuarios anónimos. Para autenticar desde la consola, debe iniciar sesión con su nombre de usuario y contraseña\. Para autenticar desde el API o la CLI, debe proporcionar su clave de acceso y clave secreta\. También es posible que tenga que proporcionar información de seguridad adicional\. AWS le recomienda el uso de la autenticación multifactor \(MFA\) para aumentar la seguridad de su cuenta\. Para obtener más información acerca de las identidades de IAM que AWS puede autenticar, consulte [Identidades \(usuarios, grupos y roles\)](id.md)\.

## Autorización<a name="intro-structure-authorization"></a>

Durante la autorización, IAM utiliza los valores del contexto de la solicitud para comprobar políticas coincidentes y determinar si permite o deniega la solicitud. Las políticas están almacenads en IAM como documentos JSON y especifican los permisos que se permiten o deniegan a entidades principales \(*políticas basadas en la identidad*\) o a recursos \(*políticas basadas en recursos*\)\.

IAM comprueba cada política que coincide con el contexto de su solicitud\. Si una política única incluye una acción denegada, IAM deniega toda la solicitud y deja de evaluarla. Esto se denomina una *denegación explícita*. Dado que las solicitudes se deniegan de *forma predeterminada*, IAM autoriza su solicitud únicamente si cada parte de su solicitud es permitida por las políticas coincidentes\. La lógica de evaluación sigue estas reglas:

+ De forma predeterminada, se deniegan todas las solicitudes\.
+ Un permiso explícito anula esta opción predeterminada\.
+ Una denegación explícita invalida cualquier permiso concedido\.

**Nota**  

De forma predeterminada, solo el [usuario raíz de la cuenta AWS](id_root-user.md) tiene acceso a todos los recursos de la cuenta\. Por lo tanto, si usted no ha iniciado sesión como usuario raíz, debe disponer de permisos concedidos por una política\.

## Acciones<a name="intro-structure-actions"></a>

Una vez que la solicitud ha sido autenticada y autorizada, AWS aprueba las acciones en su solicitud. Las acciones se definen mediante un servicio y son las cosas que usted puede hacer en un recurso, como visualizar, crear, editar y eliminar dicho recurso. Por ejemplo, IAM admite unas 40 acciones para un recurso de usuario, incluidas las siguientes acciones:

+ `CreateUser`
+ `DeleteUser`
+ `GetUser`
+ `UpdateUser`

Para permitir a una entidad principal realizar una acción, usted debe incluir las acciones necesarias en una política que se aplica a la entidad principal o al recurso afectado\.

## Recursos<a name="intro-structure-resources"></a>

Después de que AWS aprueba las acciones en su solicitud, dichas acciones pueden realizarse en los recursos relacionados dentro de su cuenta\. Un recurso es una entidad que existe dentro de un servicio\. Entre los ejemplos se incluyen una instancia Amazon EC2, un usuario de IAM y un bucket de Amazon S3\. El servicio define un conjunto de acciones que se pueden llevar a cabo en cada recurso\. Si usted crea una solicitud para llevar a cabo una acción independiente en un recurso, dicha solicitud se deniega\. Por ejemplo, si solicita eliminar un rol IAM pero proporciona un recurso de grupo de IAM, la solicitud falla\.

Cuando usted proporciona permisos utilizando una política basada en identidades en IAM, entonces usted proporciona permisos para acceder a los recursos únicamente dentro de la misma cuenta\. Si necesita realizar una solicitud en otra cuenta, el recurso en dicha cuenta debe tener una política basada en recursos adjunta que permita el acceso desde su cuenta\. De lo contrario, usted debe asumir un rol dentro de dicha cuenta con los permisos que necesita\. Para obtener más información sobre los permisos entre cuentas, consulte [Conceder permisos entre cuentas de AWS](access_permissions-required.md#UserPermissionsAcrossAccounts)\.