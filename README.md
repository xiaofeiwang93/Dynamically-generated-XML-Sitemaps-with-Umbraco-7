# Dynamically generated XML Sitemaps with Umbraco 7

1. Create a new Template
First, I create a new template named “XML Sitemap” with no parent layout. I create the template in the Umbraco back office and then add the .cshtml file to the project where I can edit it with Visual Studio. I’ve modified the original script so that it works as a View.

2. Create a new Document Type
Next I create a new Document Type also named “XML Sitemap.” I deselect the option to create a matching template since I already created one. I select “XML Sitemap” as the only allowable and the default template. I also add a property called “Hide in XML Sitemap” (alias: hideInXmlSitemap) to the XML Sitemap document type and any other Document Types I might want to exclude from the sitemap. To make it polished, I select the Sitemap icon for the document type.

3. Create the Sitemap node
Before we create the content node we need to modify the Home Document Type so that it allows for the creation of child nodes of the type XML Sitemap. Then create the node under Home with the type of XML Sitemap and check the “Hide in XML Sitemap” property.

4. Update Robots.txt to specify XML Sitemap location
The sitemap should now be loadable at sitename.com/sitemap/. However, unless the sitemap is at /sitemap.xml, Google (and other search crawlers) won’t know where to find it. To make it discoverable, add a line like the following to robots.txt:
Sitemap: http://www.alexlindgren.com/sitemap/
Note that according to the spec, this must be a full URL.

Reference: https://www.alexlindgren.com/posts/dynamically-generated-xml-sitemaps-with-umbraco-7/

5. In the Web.config, add rewrite rule: 
    <rewrite>
      <rules>
        <!-- Redirect rule for /sitemap.xml into /sitemap -->
        <rule name="SiteMap" patternSyntax="Wildcard" stopProcessing="true">
          <match url="sitemap.xml" />
          <action type="Redirect" url="sitemap" appendQueryString="false" redirectType="Permanent" />
        </rule>
      </rules>
    </rewrite>
    
