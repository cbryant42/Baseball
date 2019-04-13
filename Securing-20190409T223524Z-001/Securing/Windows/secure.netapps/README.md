# Security Aspects for a Web Application

1. Remove the Server version headers in the web.config
	```
	<system.web>
		<httpRuntime enableVersionHeader="false" />
	</system.web>
	```

2. Disable version header in the Global ASAX file in web application
	```
		MvcHandler.DisableMvcResponseHeader = true;
	```
3. Remove the CORS policy that allows * for any URL, any header and any method

4. Disable debug
	publish using the default release config, use the following
	```
	<system.web>
		<compilation debug=”false“>
	```
5. Disable the directory browsing
	```
	<system.webServer>
	  <directoryBrowse enabled="false" />
	</system.webServer>
	```

6. Use Custom errors
	```
	FOR IE 6
	<customErrors mode="On">
		<error code="404" path="404.html" />
		<error code="500" path="500.html" />
	</customErrors>
	FOR IE 7+
	<httpErrors errorMode="Custom">
	  <remove statusCode="404"/>
	  <error statusCode="404" path="/404.html" responseMode="ExecuteURL"/>
	</httpErrors>
	```
7. Set all cookies to be secure using AlwaysSecure option in the CookieAuthenticationOptions 
	```
	<system.web>
		<httpCookies httpOnlyCookies=”true“>
	```
8. Use the same origin headers [Reference: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options]
	```
	<system.webServer>
	  ...
	  <httpProtocol>
		<customHeaders>
		  <add name="X-Frame-Options" value="SAMEORIGIN" />
		</customHeaders>
	  </httpProtocol>
	  ...
	</system.webServer>
	```

9. Try to host the applications over HTTPS and use HSTS along with the URL Rewrite for HTTP to HTTPS
	```
	 <system.webServer>
		<rewrite>
			<rules>
		<rule name="HTTP to HTTPS redirect" stopProcessing="true">
				<match url="(.*)" />
			<conditions>
			  <add input="{HTTPS}" pattern="off" ignoreCase="true" />
			</conditions>
		  <action type="Redirect" redirectType="Found" url="https://{HTTP_HOST}/{R:1}" />
		</rule>
			</rules>
		</rewrite>
	</system.webServer>
	```
10. Never use session in Web Api

11. Disable tracing unless for tracing any temporary issue
	```
	<system.web>
		<trace enabled=”false” localOnly=”true“>
	```
12. Never pass the user inputs to the DB without Parameterized Query

13. Always use the Antiforgery token in all posts [Form post / AJAX post / Logoff etc...]
