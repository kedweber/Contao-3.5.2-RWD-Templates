# Contao 3.5.2 CMS & Responsive Web Design \(RWD\)

## Introduction

This project will contain, among other component and widget developments, a Responsive Web Design \(RWD\) Theme.

While the latest copy of the [Contao CMS](https://contao.org) server, at the time of this writing, is 4.0.2 this project has remained in the older version. 
This is partly due to both the lack of documentation and the fact that the mechanics have been completely revamped to use the 
[Symfony2](https://symfony.com) framework and no longer Contao's own proprietary code.

Contao was produced in Germany and has the added advantage to the German's by having a number of their official documenations available in the local 
language. Of course, their English documentation is also extensive. This is an alternative to using [WordPress](https://wordpress.com/) 
and/or [Joomla!](http://www.joomla.org) CMSes.

## REQUIREMENTS

* [Web Server](http://httpd.apache.org) \(e.g. Apache or IIS\)
* MySQL 5.0.3 \(minimal support\)
* [PHP 5.3.7](http://php.net) \(minimal support\)
* PHP Additional Modules
    * GDlib \(image resizing\)
    * DOM \(XML file support\)
    * SOAP \(Extension Repository\)
    * Phar \(for internal Live Update engine\)
    * mbstring \(optional, but highly advised when dealing with multi-byte character sets\)
    * mcrypt \(optional for data encryption\)
* [Contao 3.5.2 CMS](http://download.contao.org) 

## Installing Contao 3.5.2 CMS

The official documentation for the installation of Contao can be found [on their documenation page](https://docs.contao.org/). 
It is briefly reiterated here for the sake of easy and summarized access. 
It will also contain additional issues that occurred during the building of this particular project. 

### [Download Contao](http://download.contao.org)

Dependent on your server configuration, the public folder can most likely be found in one of the following 4 directories;
`htdocs`, `httpdocs`, `html` or `public_html`.

### Database Connectivity

The following step will require you to enter your login credentials; therefore, we should first create a database for your Contao 
website. Note that Contao's default character set is spelled as `UTF-8` while with MySQL that would be writen as `UTF8`.  

### Contao Installation Tool

The `install.php` script in the root of your Contao website can be used to help automate your installation. In the event that you mistype 
your password three times, Contao will lock down the system. Should this occur, then you will manually be required to remove the lock 
with a text editor located in the following file; 
 `system/config/localconfig.php`. 
 Within this file, you will have to set the following code to the value of 0.

```php
$GLOBALS['TL_CONFIG']['installCount'] = 0; //This will reset your attempts to 0 allowing another 3 attempts
```

### Updating the Database Tables

During the installation process, we are not only requested for the credentials, connectivity and name of your database, but 
you will also receive suggestions about altering your database tables. This is more likely to occur when upgrading your Contao, while using 
a legacy database.

### Themes \(aka. Website Design or Style\)

Here we casual go over Themes and Templates as the focus is now installation. Please see the Themes and Frontend Templates 
for more information.

WARNING: Importing a template will replace existing data. Since version 3.2.11 the sample web-page is no longer distributed with the core 
download. There are two optional manners to download the older templates 
[Contao Official Demo](https://contao.org/en/extension-list/view/official_demo.en.html) or the old 
[Music Academy](https://contao.org/en/extension-list/view/music_academy.en.html) can be installed as an extension.

* Installation of the Demos
    * Create a new Contao installation with the admin account
    * Log in as admin to the backend
    * Install the matching extension from the extension repository
    * Log out of the backend 
    * Open the install.php tool again

To import the template, select the entry from the drop-down menu and click the "Import template" button.

### An Admin User Account

NOTE: The administrative backend will be your server's administrative directory plus /contao \(i.e. http://localhost/contao\).

Interesting thing about the documentation, it says that if you did not import a template \(theme\) then you are required to create 
an administrative account in order to complete the installation process. Otherwise, if you are using the 
[example website](https://contao.org/en/extension-list/view/official_demo.en.html) then you would use the user name supplied there in:
* **User Name** : `k.jones`
* **Password** : `kevinjones`

@TODO add a link or mention about creating a template from scratch to this section.

### User-Friendly URLs or Semantic URLs \(Slugs\) 

Basically, both are fairly similar with few differences. Both are viewed as handy for Search Engine Optimisation (\SEO\) and eventually 
for bring more visitors to your site. Some systems define a `slug` as the part of a URL which identifies a page using human-readable keywords. 
It is usually the end part of the URL, which can be interpreted as the name of the resource, similar to the basename in a filename or the title of a page.

There are multiple ways to accomplish this. When using the [Apache Web Server](http://httpd.apache.org) in unison with Contao, 
you can use the `mod_rewrite` \(module plugin for Apache that rewrites URLs automatically\), which is configured in the Apache's `.htaccess` 
file. Contao uses a file named `.htaccess.default` found in it's root directory. If you can't configure that manually, 
 you will want to move or rename the Contao default settings to just a normal `.htaccess` file and do the following. 
 NOTE: On POSIX systems, files beginning with a period are hidden from normal file viewers.  
Select the "Rewrite URLs" in the "Front end configuration" section and save your work. Now Contao will generate static URLs like 
`home.html` instead of `index.php?id=12`.

**KEYWORDS :** [Reciprocal Links](http://www.webconfs.com/reciprocal-link-checker.php), [BackLinks](http://www.backlinks.com/), 
Link Exchanges, trackback_url\(\) for WordPress, mod_rewrite, 301 Redirects, Pingback \(a link contained in a post\).


### File Permissions \(aka. Safe Mode Hack\)

Briefly, to overcome issues with PHP having write access to certain directories, while running the install.php script mentioned above 
Contao will set permissions to `chmod 777`, giving write and execute permission to the following directories every system user and they 
strongly advise against making changes to these settings;

* assets/images
* assets/images/*
* system/logs
* system/tmp

The back-end of Contao expects you to be running an File Transfer Protocol \(FTP\) server and allows you to modify your files via PHP's FTP functions.

### Backups Before Upgrades

Backing up the following files and two directories will save your local configuration, custom templates and files.

* files/*
* system/config/dcaconfig.php
* system/config/initconfig.php
* system/config/langconfig.php
* system/config/localconfig.php
* templates/*

**Attention:** If you have installed any third-party extensions, make sure to backup and restore them, too, or do not overwrite them at all. 
Otherwise, you will need to reinstall the modules and depending on the behavior of the extension you could run the risk of losing valuable data.

### Rebuild Cached Language and DCA Files

In the back-end you can go to "Maintenance", check "Purge the internal cache" in the "Purge data" section. After a 
subsequent confirmation that you wish to purge data, you will need to click the "Build the cache" in the header. 

### Live Update pg 12


# Themes and Frontend Templates

A website design is normally controlled by the following elements; stylesheets, frontend modules \(that which the visitor of the website sees\), 
page layouts (controlled by HTML and stylesheets\), files \(e.g. javascript, images and videos\) and templates. The integrated *theme manager* 
 does not change the common approach to separating the elements of a website. 

The Contao CMS' backend has interfaces for dealing with all these elements. As we mentioned before, Contao likes to side-step possible user rights issues by 
providing an integrated FTP client for modifying and uploading files.

## Themes Versus Frontend Templates

The main difference between a *theme* and a *frontend template* is that the later contains a fully preconfigured example 
 website. That's right, the *template* includes such things as an exemplary site-structure, articles, content elements and 
 even preconfigured users and user-groups. In comparison, a *theme*, consists only of the actual website design; this gives it the 
advantage of not overwriting existing data when imported.

## Components of a Theme \(and the Theme Configuration Tool\)

With the Theme Configuration Tool one is capable of exporting a Theme which has been created or import one from a file name ended 
with `.cto`. A CTO file is simply a compiled .zip file, so one can change the name and examine the contents of said compiled import/export files. 
Realize that these `.cto` files are comprised of **Theme components**.
 
Importing a theme does not endanger your current data; however Frontend Templates would. In order to import the .cto file to your Contao 
installation, you will need to open the Theme Manager and click on the link labeled "Theme import". You can import multiple themes at once. 
Once the import process is completed, you may then assign the page layout(s) of the new theme in the site structure.

**Theme components** are stored within the database instead of via flat-files;

* Style Sheets \(nomenclature prefix standards: "ce_" for Content Elements and "mod_" for Module classes\)
* FrontEnd Modules
* Page Layouts \(determine the basic layout of the page, which components are shown where\)

while of course it can also use flat-files, such as the following which would need to be coupled onto the theme within the backend theme configuration tool 
in order to assure they are included in any theme exports;

* Images
* Files such as optional custom templates from the templates directory

Within the "Theme Configuration Tool" one must specify the title and author. Additional folders to include can be added optionally, 
as well as a screenshot and the path to a "templates" folder. Finally, something that Contao seems to make use of more than other 
CMSes is *Global Variables*. Within the tool, you can pack your theme with additional variables to be available over the entire site.

Contao also supplies a style sheet editor in the backend CMS.


# Modules

## Access Control 

As similar to the CCK's Access Control, Contao also affords individual module access control. Each frontend module can be 
protected so only guests or memembers of a particular user's group can see it on the website; if deemed so necessary.

## Reference Listing

| Module | CSS Class | Description  |
| ------------------- | ----------- | ------ |
| Navigation Menu | mod_navigation | Generates a navigation menu from the site structure. |
| Custom Navigation | mod_costomnav | Geerates a custom navigation menu. |
| Breadcrumb Navigation | mod_breadcrumb | Generates a breadcrumb navigation menu. |
| Quick Navigation | mod_quicknav | Generates a drop-down menu from the site structure. |
| Quick Link | mod_quicklink | Generates a custom drop-down menu. |
| Book Navigation | mod_booknav | Generates a book navigation menu. |
| Article Navigation | mod_article_nav | Generates a pagination menu to navigate the articles. |
| Sitemap | mod_sitemap | Generates a list of all pages in the site structure. |
| Login Form | mod_login | Generates a login form \(Should be compared to the "God Form" login\). |
| Automatic Logout | - | Automatically logs the user out. |
| Personal Data | mod_personalData | Generates a form that allows one to edit one's personal data. | 
| Registration | mod_registration | Generates a user registration form. |
| Change Password | mod_changePassword | Generates a form to change a user's password. |
| Lost Password | mod_password | Generates  a form for requesting a new password. |
| Close Account | mod_closeAccount | Generates a form to delete a member account. |
| Newslist | mod_newslist | Adds a list of news items to the page. |
| Newsreader | mod_newsreader | Shows the details of a news item. |
| News Archive | mod_newsarchive | Adds a news archive to the page. |
| News Archive Menu | mod_newsmenu | Generates a navigation menu to browse the news archive(s). |
| Calendar | mod_calendar | Adds a calendar to the page. |
| Event Reader | mod_eventreader | Shows the details of an event. |
| Event List | mod_eventlist | Adds a list of events to the page. |
| Event List Menu | mod_eventmenu | Generates a navigation menu to browse the event list. |
| Subscribe | mod_subscribe | Generates a form to subscribe to one or more channels. |
| Unsubscribe | mod_unsubscribe | Generates a form to unsubscribe from one or more channels. |
| Newsletter List | mod_nl_list | Adds a list of newsletters to the page |
| Newsletter reader | mod_nl_reader | Shows the details of a newsletter. |
| FAQ List | mod_faqlist | Adds a list of frequently asked questions to the page. |
| FAQ Reader | mod_faqreader | Shows the answer to a frequently asked question. |
| FAQ Page | mod_faqpage | Shows the FAQ list and the FAQ reader on the same page. |
| Form | mod_form | Adds a form to a page. | 
| Search Engine | mod_search | Adds a search form to a page. |
| Comments | mod_comments | Manage comments or a guestbook entries. |
| Listing | mod_listing | Lists the records of a table. |
| Flash Movie | mod_flash | Embeds a Flash movie into a page. |
| Article List | mod_article_list | Generates a list of articles of a column. |
| Random Image | mod_random_image | Adds a random image to a page. |
| Custom HTML | - | Allows you to add custom HTML code. |
| RSS reader | mod_rss_reader | Adds an RSS feed to a page. |


