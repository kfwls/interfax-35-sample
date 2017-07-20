# Sample

Full buildable solution also provided in this repository.

```csharp
using System;
using System.Collections.Generic;
using System.Net;
using System.Text;

namespace Interfax_35_sample
{
	class Program
	{
		static void Main(string[] args)
		{
			const string username = "";
			const string password = "";
      
			const string faxFilePath = "test.pdf";
			const string destinationFaxNumber = "+449999999999";
			const string baseUri = "https://rest.interfax.net";

			string uploadUri = "/outbound/faxes";

			// Instatiate a web client
			WebClient webClient = new WebClient();

			// Add required configuration options
			Dictionary<String, String> options = new Dictionary<string, string>();
			uploadUri += "?" + "faxNumber" + "=" + destinationFaxNumber.Replace("+", "%2b");

			// Add Authentication and Headers
			var encodedAuth = Convert.ToBase64String(Encoding.ASCII.GetBytes(username + ":" + password));
			webClient.BaseAddress = baseUri;
			webClient.Headers.Add(HttpRequestHeader.Authorization, "Basic " + encodedAuth);
			webClient.Headers.Add(HttpRequestHeader.Accept, "application/json");
			webClient.Headers.Add(HttpRequestHeader.ContentType, "application/pdf");

			// Submit
			var result = webClient.UploadFile(uploadUri, "post", faxFilePath);
		}
	}
}
```
