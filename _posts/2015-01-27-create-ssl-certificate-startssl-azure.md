---
layout: post
title: Creating a StartSSL SSL Certificate for Azure
excerpt: "Here are the steps to create a StartSSL ssl certificate for use on an Azure website."
tags: [nuget, package manager, open source]
modified: 2015-01-24
comments: true
---

Creating an SSL certificate for a website is a necessary task, but one may be infrequently completed. Because of this I always seem to forget how to generate and install my SSL certificate properly. StartSSL has been my go to certificate authority because of the suggestions by [Troy Hunt](http://www.troyhunt.com/2013/09/the-complete-guide-to-loading-free-ssl.html). They are very inexpensive however their website isn't the most intuitive. That being said I usually forget the steps I need to follow to create an SSL cert for a new site so as a reminder I created these quick and dirty steps for creating and using a certificate with StartSSL for an Azure website. I am not security expert so comment below if you know of a better or more secure method.

1. Generate StartSSL Cert
  * Authenticate with [http://startssl.com](http://startssl.com)
  * Go to the Certificates Wizard tab, choose the web server target and continue
  * Choose and confirm a password, select the largest key size, select SHA2 and continue
  * Save your generated private key and continue
  * Select your domain. (You should have validated a domain at this point)
  * Select the domain and sub-domain you want to use (typically domain.com and www.domain.com) and continue
  * Continue and wait for approval
  * Go to the Tool Box tab and click Retrieve Certificate
  * Select the certificate you want to retrieve and continue
  * Save your certificate
1. Generate the PFX for Azure (note: this may not be the most secure way to generate the pfx, but it works for me)
  * Go to the Tool Box tab and click on Create PKCS#12
  * Enter your private key, certificate and password for the private key and continue
  * Get PFX and the p12 file will be downloaded to your computer
  * Change the file extension to .pfx http://akbarahmed.com/2011/11/04/convert-p12-to-pfx/
1. Add PFX to Azure
  * Open the Azure portal
  * Select the website you need the cert on
  * Click on the configure tab
  * Click upload certificate and find your pfx and enter the private key password and continue
  * If all goes well your certificate is now available for your website
  * Under SSL Bindings choose your domain to secure, choose the certificate you just uploaded and choose the ssl type. (IP Based is only available for Standard hosting)
  * Repeat for all domains that need to be secured.
  * Save

I started this process when I needed to swap my old SHA1 cert to a SHA256 cert. After installing the cert and setting it in the portal my site still served the old cert. I thought it was a bug in the portal and tried to restart my server, stop it and start it and delete the old cert (didn't work because I had another server using it), but I still thought that there was a bug in Azure so I created a post on their forum in hopes that someone would help me out. After creating my post I noticed a "Search related threads" link at the top of the page that lead me to this thread [Sporadic wrong certificate being served](https://social.msdn.microsoft.com/Forums/azure/en-US/58de9b0d-da5b-4bd6-8b75-8be10a3a3553/sporadic-wrong-certificate-being-served?forum=windowsazurewebsitespreview) This thread suggested that your A record IP needs to match the virtual IP given to the website. I had overlooked this point an as soon as I set my A record correctly the correct certificate was serve.

Another setback I experienced was that StartSSL was using a SHA1 intermediate certificate. I didn't really know how intermediate certificates worked so I leveled up my knowledge [here](https://forum.startcom.org/viewtopic.php?f=15&t=15741) Unfortunately I haven't been able to figure out how to remove the old intermediate certificate without re-creating a new website. I'll update this as soon as I get some support from Azure.

Update: I guess this was an Azure bug. Eventually my site was updated and it started serving the correct intermediate certificate. All is well.

<!---
{% highlight css %}
#container {
    float: left;
    margin: 0 -240px 0 0;
    width: 100%;
}
{% endhighlight %}

{% highlight html %}
{% raw %}
<nav class="pagination" role="navigation">
    {% if page.previous %}
        <a href="{{ site.url }}{{ page.previous.url }}" class="btn" title="{{ page.previous.title }}">Previous article</a>
    {% endif %}
    {% if page.next %}
        <a href="{{ site.url }}{{ page.next.url }}" class="btn" title="{{ page.next.title }}">Next article</a>
    {% endif %}
</nav><!-- /.pagination -->
{% endraw %}
{% endhighlight %}

{% highlight ruby %}
module Jekyll
  class TagIndex < Page
    def initialize(site, base, dir, tag)
      @site = site
      @base = base
      @dir = dir
      @name = 'index.html'
      self.process(@name)
      self.read_yaml(File.join(base, '_layouts'), 'tag_index.html')
      self.data['tag'] = tag
      tag_title_prefix = site.config['tag_title_prefix'] || 'Tagged: '
      tag_title_suffix = site.config['tag_title_suffix'] || '&#8211;'
      self.data['title'] = "#{tag_title_prefix}#{tag}"
      self.data['description'] = "An archive of posts tagged #{tag}."
    end
  end
end
{% endhighlight %}
-->