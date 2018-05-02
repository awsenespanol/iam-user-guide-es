# ¿Qué es IAM??<a name="introduction"></a>

AWS Identity and Access Management \(IAM\) es un servicio web que le ayuda a controlar de forma segura el acceso a los recursos de AWS\. Utilice IAM para controlar quién está autenticado \(ha iniciado sesión\) y autorizado \(tiene permisos\) para utilizar recursos\.

Cuando usted crea por primera vez una cuenta de AWS, comienza con una identidad de inicio de sesión única que tiene acceso completo a todos los servicios y recursos de AWS en la cuenta\. Esta identidad recibe el nombre de *usuario raíz* de la cuenta de AWS y se obtiene acceso a ella iniciando sesión con la dirección de correo electrónico y la contraseña que utilizó al crear la cuenta\. Le recomendamos que no utilice el usuario raíz en sus tareas cotidianas, ni siquiera en las tareas administrativas\. En lugar de ello, es mejor ceñirse a la [práctica recomendada de utilizar el usuario raíz exclusivamente para crear el primer usuario de IAM](http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#create-iam-users)\. A continuación, guarde las credenciales del usuario raíz en un lugar seguro y utilícelas únicamente para algunas tareas de administración de cuentas y servicios\.

**Temas**
+ [Vídeo de introducción a IAM](#intro-video)
+ [Características de IAM](#intro-features)
+ [Acceso a IAM](#intro-accessing)
+ [Entender cómo funciona IAM](intro-structure.md)
+ [Introducción a la administración de identidades: usuarios](introduction_identity-management.md)
+ [Información general sobre la administración del acceso: permisos y políticas](introduction_access-management.md)
+ [Características de seguridad fuera de IAM](introduction_security-outside-iam.md)
+ [Enlaces rápidos a tareas comunes](introduction_quick-links-common-tasks.md)

## Vídeo de introducción a IAM<a name="intro-video"></a>

La capacitación y certificación de AWS ofrece una introducción en vídeo de 10 minutos a IAM::

[Introducción a AWS Identity and Access Management](https://www.aws.training/learningobject/video?id=16448)

## Características de IAM<a name="intro-features"></a>

IAM le ofrece las siguientes características:

**Acceso compartido a la cuenta de AWS**  
Usted puede conceder permiso a otras personas para administrar y utilizar los recursos de su cuenta de AWS sin tener que compartir su contraseña o clave de acceso\.

**Permisos detallados**  

Usted puede conceder diferentes permisos a diferentes personas para diferentes recursos\. Por ejemplo, puede permitir que algunos usuarios tengan acceso completo a Amazon Elastic Compute Cloud \(Amazon EC2\), Amazon Simple Storage Service \(Amazon S3\), Amazon DynamoDB, Amazon Redshift y otros servicios de AWS\. En el caso de otros usuarios, puede permitir el acceso de solo lectura a solo algunos buckets de S3 o conceder permiso para administrar solo algunas instancias EC2 o para tener acceso a la información de facturación, pero nada más\.

**Acceso seguro a los recursos de AWS para aplicaciones que se ejecutan en Amazon EC2**  

Usted puede utilizar características de IAM para proporcionar de forma segura credenciales para las aplicaciones que se ejecutan en instancias EC2\. Estas credenciales proporcionan permisos a su aplicación para obtener acceso a otros recursos de AWS. Entre los ejemplos se incluyen buckets de S3 y tablas de DynamoDB\.

**Multi\-factor authentication \(MFA\)**  

Usted puede agregar una autenticación de dos factores a la cuenta y a los usuarios individuales para mayor seguridad\. Con MFA usted o sus usuarios deben proporcionar no solo una contraseña o clave de acceso para trabajar con la cuenta, sino también un código de un dispositivo especialmente configurado\.

**Identidad federada**  

Usted puede permitir a los usuarios que ya tienen contraseñas en otros lugares, por ejemplo, en su red corporativa o con un proveedor de identidades de Internet, obtener acceso temporal a su cuenta de AWS\.

**Información de identidad para realizar un control**  

Si usted utiliza [AWS CloudTrail](https://aws.amazon.com/cloudtrail/), recibirá registros de logs que incluyen información sobre los usuarios que realizan solicitudes de recursos en su cuenta\. Esta información se basa en identidades de IAM\.

**Conformidad con DSS de PCI**  

IAM admite el procesamiento, el almacenamiento y la transmisión de datos de tarjetas de crédito por parte de un comerciante o proveedor de servicios, y ha sido validado para estar conforme con el Estándar de Seguridad de los Datos de la Industria de las Tarjetas de Pago \(DSS PCI\)\. Para obtener más información acerca de PCI DSS, incluido cómo solicitar una copia de AWS PCI Compliance Package, consulte [PCI DSS nivel 1](https://aws.amazon.com/compliance/pci-dss-level-1-faqs/)\.

**Integración con muchos servicios de AWS**  

Para obtener una lista de servicios de AWS que funcionan con IAM, consulte [Servicios de AWS que funcionan con IAM](reference_aws-services-that-work-with-iam.md)\.

**Eventualmente consistente**  

IAM, al igual que muchos otros servicios de AWS, ofrece [consistencia consistente](https://wikipedia.org/wiki/Eventual_consistency)\. IAM consigue una alta disponibilidad replicando datos entre varios servidores ubicados en centros de datos de Amazon de todo el mundo\. Si una solicitud para cambiar algunos datos se realiza correctamente, el cambio se confirma y se almacena de forma segura\. Sin embargo, el cambio se debe replicar en IAM, lo que puede llevar algún tiempo. Estos cambios incluyen la creación o actualización de usuarios, grupos, roles o políticas\. Le recomendamos que no los incluya tales cambios de IAM en las rutas de código de gran importancia y alta disponibilidad de su aplicación\. En su lugar, realice los cambios de IAM en otra rutina de inicialización o configuración que ejecute con menos frecuencia\. Además, asegúrese de comprobar que los cambios se hayan propagado antes de que los flujos de trabajo de producción dependan de ellos\. Para obtener más información, consulte [Los cambios que yo realizo no están siempre visibles inmediatamente](troubleshoot_general.md#troubleshoot_general_eventual-consistency)\.

**Uso gratuito**  

AWS Identity and Access Management \(IAM \) y AWS Security Token Service \(AWS STS \) son características de su cuenta de AWS ofrecidas sin cargo adicional. Se le cobrará solo cuando acceda a otros servicios de AWS utilizando sus usuarios de IAM o credenciales temporales de seguridad de AWS STS. Para obtener información sobre el precio de otros productos de AWS, consulte la [página de precios de Amazon Web Services](https://aws.amazon.com/pricing/)\.

## Acceso a IAM<a name="intro-accessing"></a>

Usted puede trabajar con AWS Identity and Access Management de cualquiera de las siguientes formas\.

**Consola de administración de AWS** 

La consola es una interfaz para el navegador para administrar los recursos de IAM y AWS\. Para obtener más información sobre cómo acceder a IAM a través de la consola, consulte [La consola de IAM y la página de inicio de sesión](console.md)\. Para ver un tutorial que le oriente en el uso de la consola, consulte [Creación del primer grupo y usuario administrador de IAM].

**Herramientas de línea de comandos de AWS**  

Usted puede utilizar las herramientas de línea de comandos de AWS para emitir comandos en la línea de comando de su sistema con el fin de llevar a cabo tareas de IAM y de AWS\. El uso de la línea de comandos puede ser más rápido y cómoda que la consola\. Las herramientas de línea de comandos también son útiles si desea crear scripts que realicen tareas de AWS\.

AWS proporciona dos conjuntos de herramientas de línea de comandos: la [AWS Command Line Interface](https://aws.amazon.com/cli/) \(AWS CLI\) y las [Herramientas de AWS para Windows PowerShell](https://aws.amazon.com/powershell/)\. Para obtener información sobre cómo instalar y usar AWS CLI, consulte [AWS Command Line Interface Guía del usuario](http://docs.aws.amazon.com/cli/latest/userguide/)\. Para obtener información sobre cómo instalar y usar Herramientas para Windows PowerShell, consulte [Guía del usuario de Herramientas de AWS para Windows PowerShell](http://docs.aws.amazon.com/powershell/latest/userguide/)\.

**SDK de AWS**  

AWS ofrece SDK \(kits de desarrollo de software\) que se componen de bibliotecas y código de muestra para diversos lenguajes de programación y plataformas \(Java, Python, Ruby, .NET, iOS, Android, etc\.\). Los SDK proporcionan una forma cómoda de crear acceso mediante programación a IAM y AWS\. Por ejemplo, los SDK se encargan de tareas como firmar solicitudes criptográficamente, gestionar los errores y reintentar las solicitudes de forma automática\. Para obtener información sobre los SDK de AWS, incluido cómo descargarlos e instalarlos, consulte la página [Herramientas para Amazon Web Services](https://aws.amazon.com/tools/) page\.

**API HTTPS de IAM**  

Usted puede acceder a IAM y AWS de manera programática usando la API HTTPS de IAM, que le permite emitir solicitudes HTTPS directamente al servicio. Cuando use la API HTTPS, debe incluir código para firmar digitalmente las solicitudes utilizando sus credenciales. Para obtener más información, consulte [Llamar a la API mediante solicitudes de consulta HTTP](programming.md) y la [Referencia API de IAM](http://docs.aws.amazon.com/IAM/latest/APIReference/)\.