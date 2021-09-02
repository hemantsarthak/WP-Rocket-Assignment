<!-- vscode-markdown-toc -->
* 1. [Issue 1](#Issue1)
	* 1.1. [Step by Step Guide:](#StepbyStepGuide:)
* 2. [Issue 2](#Issue2)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->
# Problem
A teammate has reached out to you to assist them with a customer’s request.
##  1. <a name='Issue1'></a>Issue 1
The customer disabled WP Rocket’s automatic cache clearing system. They want you to provide them with a way to clear the following cache files at a specific time they select, e.g. when the site has the least traffic:
*	HTML
*	Combined/minified CSS/JavaScript files

Using WP Rocket’s existing functions:
1.	Explain how they should implement the requirement to clear the cache at a specific time.
2.	Provide any piece of code necessary to perform the cache clearing task.

# Solution 1
Hello Name,
Hope you are doing well, as for your query to clear the cache at a specific time you will have to create a cron job with the following code:
```
<?php 
// Load WordPress.
require( 'wp-load.php' );

// Clear cache.
if ( function_exists( 'rocket_clean_domain' ) ) {
	rocket_clean_domain();
 }
 ```
 > **Note:** If you place it in a different location then root, you need to edit the path in require( 'wp-load.php' ); above to match its location. 
 
Set up to run when your site have the lowest amount of visitors based or any time you desire.

You can use the tool [Crontab-generator](https://crontab-generator.org/) to set up timings for the cron job if you are using UNIX/SERVER based cron jobs via cPanel etc.

If you want to use wp-cron these two plugins should help:
*	Check if WP-Cron is Available on your website using [WP Cron Status Checker](https://wordpress.org/plugins/wp-cron-status-checker/).
*	Easily setup WP-Cron Using [WP Crontrol](https://wordpress.org/plugins/wp-crontrol/) or [Advanced Cron Manager](https://wordpress.org/plugins/advanced-cron-manager/).

##### WP Rocket Resources:
[Cache Clearing via Cron Job](https://docs.wp-rocket.me/article/494-how-to-clear-cache-via-cron-job)
[Cron Jobs EXPLAINED & Creation Guide](https://docs.wp-rocket.me/article/1279-cron-and-wp-rocket#setting-up-cron-job)

###  1.1. <a name='StepbyStepGuide:'></a>Step by Step Guide: 
Here is a detailed guide that you can follow as well:
##### Creating a Cron Job
1.	Create a php file named **rocket-clean-domain.php**. You can use a notepad or any code editor you want.
2.	Add this code in the file & save it
```
<?php 
// Load WordPress.
require( 'wp-load.php' );

// Clear cache.
if ( function_exists( 'rocket_clean_domain' ) ) {
	rocket_clean_domain();
 }
 ```
  > **Note:** If you place it in a different location then root, you need to edit the path in require( 'wp-load.php' ); above to match its location. 
  
3.	Upload this file to the root WordPress folder (it’s the folder [where wp-config.php and wp-load.php are located](https://recordit.co/jbtM0WPfcw)).
To upload the file the you can either:
*  **Use FTP to add the file**
The credentials for the FTP will be present at different places based on your hosting provider.
    * Here are guides for some hostng providers dashboards:
        1. [Kinsta](https://kinsta.com/knowledgebase/how-to-use-sftp/ )
        2. [WP Engine](https://wpengine.com/support/sftp/)
        3. [cPanel](https://help.liquidweb.com/s/article/Uploading-Files-Using-FTP-in-cPanel)
        4. [Cloudways](https://support.cloudways.com/en/articles/5119485-guide-to-connecting-to-your-application-using-ssh-sftp)
    * After getting access to the FTP just add the **rocket-clean-domain.php file** as shown [in this video](https://recordit.co/jbtM0WPfcw). 
    
    If you have any other hosting provider that we missed please let us know we will try to provide you a custom guide for that platform, or you can contact your hosting provider support for your FTP credentials as well. 
* **Using a File Manager Plugin**
If you can’t access your FTP credentials etc. you can use a WordPress File Manager like [WP File Manager](https://wordpress.org/plugins/wp-file-manager/) or any other reputed file manager you like and add the file thrugh them as well:
    1. After Installing & Activating the Plugin Go to file manager
    ![File Manager](https://i.imgur.com/YoT3oQi.png)
    2. You will get a file explorer like this
    ![File Explorer](https://i.imgur.com/m6wVxp4.png)
    3. Ensure that you are in the root directory & create a new file (it’s the folder [where wp-config.php and wp-load.php are located](recordit.co/jbtM0WPfcw)).
    ![New File](https://i.imgur.com/QuPi5uo.png)
    4. Rename the file **rocket-clean-domain.php file** & open the code editor
    ![Code Editor](https://i.imgur.com/93X7S9o.png)
    5. Add the code mentioned at the top, save & close.
    ![Save Code](https://i.imgur.com/5LVl0F8.png)
You have sucessfully created a cron job script, now lets schedule it & run it.

    
##### Scheduling a Cron Job
Before proceding, please read the [**difference between WP Cron & Real Cron**](https://docs.wp-rocket.me/article/1279-cron-and-wp-rocket#wp-cron-vs-real-cron).

You have three options that you can use to create a cron job:

1. **Using Real Cron Jobs**
    1. If you want to create a Real/Server Cron job, first you need to disable WP Cron, so is not executed every time someone loads one of your webpages. 
    To disable it, open the wp-config.php file in your main WordPress folder and add the following line before the `"/* That's all, stop editing! Happy blogging. */"` line:
`define('DISABLE_WP_CRON', true);`
Detailed guide to [disable WP Cron](https://kinsta.com/knowledgebase/disable-wp-cron/).
    2. There are different ways to add a Cron Job based on the hosting provider you are using. Here are Some Guides:
        * [Kinsta/SSH](https://kinsta.com/knowledgebase/how-to-write-a-cron-job/) - You can use [Crontab Generator](https://crontab-generator.org/) to set up timings for the cron job.
        * [WP Engine]() - They don’t support cron directly but have their own cron alternative system.
        * cPanel - [Video Guide]() and [WP Rocket Cron Job Guide]()
        * [Cloudways]()
2. **Using External Cron Services** (Easiest)
Instead of using your own hosting provider/server for the cron job you can use various external services to set up the cron job as:
    1. [Easy Cron](https://www.easycron.com/) (Freemium)
    [Easy Cron](https://www.easycron.com/) is a service that lets you create cron jobs easily. The free plans let you create cron jobs that run every 20 mins. 
Just create an account and enter your cron job address with time intervals like 
Path/URL  http://www.example.com/path/to/wp/installation/root/rocket-clean-domain.php
![Easy Cron](https://i.imgur.com/Pabh5N5.png)
Guide for [Easy Cron External Cron Setup](https://www.easycron.com/cron-job-tutorials/how-to-set-up-cron-job-for-wordpress)
    
        2.[Cron-Job](https://cron-job.org/en/) (Free)
You can use cron-job.org to add a cron job for a minute by minute to yearly basis.
Simply create an account and add the URL for cron job like: http://www.example.com/path/to/wp/installation/root/rocket-clean-domain.php
![CronJob](https://i.imgur.com/JwUNGFH.png)

    Set the time & enjoy your automated cache cleaning system!

3. **Using WP Cron**
WP-Cron is not actually a real cron job, you can think it is more like a “fake cron job”. These tasks are triggered when someone visits your site: during PHP page loads, WP Cron checks the database to see if there are any scheduled tasks to execute. 
The way WP Cron works has some drawbacks:
    *	When you are using a caching plugin like WP Rocket, no PHP is executed in the frontend, so if there is no activity on WP Admin for some time, WP Cron processes would stop being triggered.
    *	It is also a potential issue on high traffic sites, since every page request might spawn a process that uses server resources
    *	This file can be used as the target of a DOS attack

    But if you want to use wp-cron to clean the WP Rocket Cache you can follow these guides:
    [Cloudways Wordpress Cron Job](https://www.cloudways.com/blog/wordpress-cron-job)
    [Kinsta Wordpress Cron Job](https://kinsta.com/knowledgebase/wordpress-cron-job/)

##  2. <a name='Issue2'></a>Issue 2
Your teammate sent your instructions and code to the customer.
They implemented them but the cache isn’t cleared.

Provide the steps that you’d follow to troubleshoot this, based on the solution you provided in Issue 1.
Assume that:
*	you have tested your code on your environment and it works fine and
*	the customer has provided you access to their site/server.

# Solution 2
I will take the following steps if I have access to the customers site/server.
1.	First if possible, I will ask the customer what process they tried to add the cron job and clear the cache.
Then I will first check if the WP Rocket is set up correctly or not, just to determine that there is no other issue present that might hamper troubleshooting down the road, after that I will check based on the process the customer took step by step.

2.	After seeing which hosting provider, the customer is using I will see if there is a documentation provided by that hosting provider for the customers problem in this case, I will check the file upload/addition of the Cron job, the path to the root folder, the code etc, first.

3.	If the cron job was added adequately then I will then check the scheduling of the cron job if its correct or not based on the process by which the customer added the scheduling.

4.	If that’s also ok then I will check if there is a plugin etc. might be limiting or stopping this function example wordfence or something in functions.php etc or any file accessibility permission issues etc. 

5.	If that is also ok I will try an external cron to run for the time being and ask Google or the Senior Technical Support at WP Rocket or the Hosting Provider Support etc. for help.

6.	If I still can’t fix it then unfortunately, I will be forced to add a external cron and use that while apologizing to the customer and forwarding the query to the senior technical support at wp rocket. 

7.	Hopefully after all this the problem will be solved, otherwise I will apologize to the customer and ask a day to fix the problem, after my shift ends I will first create a website and test the cron on the same hosting provider as the customer, if it works then I will be assured that I might be missing something on the WP Admin Plugins etc. itself and will try to solve it or maybe even clone the website if the customer allows to my website on the same hosting provider so that I can fix it by removing plugins etc. to determine the cause and fix it and hopefully by this time it will be fixed. 

# Long Term Solution
I might be totally wrong about this appproach, but I think we can add the automatic cache cleaning at a specific time in the WP Rocket Plugin itself, or create a smaller plugin just for this function containing the bare minimum in beta for those who need this feature.

This feature can be implemented by capturing the cron job location and of loading the task to WP Cron or more likely to Easy Cron or Cron-Job.org,

This fetaure if using third paprty service will only be available to RocketCDN users as an extra bonus.

Here is the basic kind of not working code, I should be able to make it work with some guidance from the Associate or Senior Developers about the testing metodologies/priorities used,WP Rocket functions & code structure.

```
// Scheduled Action Hook 
 
function user_auto_flush_cache( ) { 
	$wp_rocket->rocket_clean_domain(); 
} 
 
//Some UI & Input
//Not added currently
//Some UI & Input
 
// Schedule Cron Job Event 
 
function input_cache_flush() { 
	if ( ! wp_next_scheduled( 'user_auto_flush_cache' ) ) { 
		wp_schedule_event( current_time( 'timestamp' ), 'daily', 'user_auto_flush_cache' );
		//daily, 18000, etc.
	} 
} 
```


# Minor Docs Update Suggestion & Demo

I noticed that the https://docs.wp-rocket.me/article/1279-cron-and-wp-rocket didn't have link or guidance to how to set the time for the cron job, I added it as demo on this like netlify.cn .

![Netlify](https://i.imgur.com/dHOeUJP.png)

# Notes
I apologize for the delayed submission, hope you will still consider me for a role at WP Rocket. Please let me know if you want me to create a full plugin for the cache auto clean as well. 
