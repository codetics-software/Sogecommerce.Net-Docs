# Sogecommerce.Net

La librairie Sogecommerce.Net est developpe par la societe Codetics. Pour pouvoir beneficier des services de Sogecommerce, il vous faudra imperativement une souscription au service aupres de la Societe Generale [https://professionnels.societegenerale.fr/compte-banque-au-quotidien/encaissement/solution-de-paiement-en-ligne](Sogecommerce). Rapprochez vous de votre conseiller pour en savoir plus sur cette offre.

# Comment ca fonctionne ?

Implementez la solution en la rajoutant � votre projet ASP.Net Core ou .Net avec NuGet.

## Integrez la librairie � votre projet

Il est tr�s simple d'int�grer la solution � votre projet. Il vous suffit pour cela d'utiliser l'extension des services ASP.Net Core dans votre fichier program.cs :

```
builder.Services.AddSogecommerce();

```

## Configurez Sogecommerce

La configuration de Sogecommerce se déroule dans votre fichier appsettings.json. La librairie est capable de reconnaitre votre environnement, il vous est donc possible de configurer vos clés en mode Test ou en mode Production en utilisant le appsettings adéquate :


```
"Sogecommerce" : {
	"SiteId" : "MON_IDENTIFIANT_BOUTIQUE",
	"ApiKey" : "MA_CLE_API"
}

```

Vous retrouverez ces informations dans votre back-office Sogecommerce. 

## Utiliser la librairie

Vous pouvez utiliser la librairie en utilisant le ViewComponent directement dans votre page Razor : 

```
@await Component.InvokeAsync("SingleInteractivePayButton", new { amount = MONTANT_ICI})

```

Le support des tag helpers arrivera dans une prochaine version de la librairie.

## Utiliser la librairie sans le composant


Vous pouvez également utiliser la librairie sans utiliser de composant. Pour cela, il vous suffit d'utiliser le service mis à disposition qui vous retournera la classe correspondante à utiliser dans vos ViewModel grâce aux dependency injection.

```
private readonly IPaymentService _paymentService;

public MyClassConstructor(IPaymentService paymentService) {
	_paymentService = paymentService;
}

public IActionResult MyAction() {
	var paymentFormModel = _paymentService.GenerateImmediatSinglePayment(10000.99);
	return View(paymentFormModel);
}

```