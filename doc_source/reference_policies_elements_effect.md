# Elementos de la política de JSON de IAM: Effect<a name="reference_policies_elements_effect"></a>

El elemento `Effect` es obligatorio y se utiliza para especificar si la declaración da como resultado un permiso o una denegación explícitos\. Los valores válidos para `Effect` son `Allow` y `Deny`\.

```
"Effect":"Allow"
```

De forma predeterminada, se deniega el acceso a los recursos\. Para permitir el acceso a un recurso, usted debe establecer el elemento `Effect` en `Allow`\. Para anular un permiso \(por ejemplo, para anular un permiso que, de lo contrario, estaría en vigor\), establezca el elemento `Effect` en `Deny`\. Para obtener más información, consulte [Lógica de evaluación de políticas de JSON de IAM](reference_policies_evaluation-logic.md)\. 