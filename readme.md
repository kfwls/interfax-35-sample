# Sample

Full buildable solution also provided in the repository.

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
			const string username = "kfwls";
			const string password = "Newjersei42";
			const string faxFilePath = "test.pdf";

			const string baseUri = "https://rest.interfax.net";
			string uploadUri = "/outbound/faxes";

			// Set configuration options
			// See https://www.interfax.net/en/dev/rest/reference/2918
			var options = new Dictionary<String, String>(){
				{"faxNumber", "+449999999999"}
			};

			// Instatiate a web client
			WebClient webClient = new WebClient();
		
			// Build url with configuration options
			uploadUri += "?";
			foreach (var x in options.Keys)
			{
				uploadUri += x + '=' + options[x] + '&';
			}

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
