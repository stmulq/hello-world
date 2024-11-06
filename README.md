# BSN.Cloud/BAconnected FAQ

#### What if my player’s serial number is already registered?

![](https://brightsign.atlassian.net/wiki/images/icons/grey_arrow_down.png)

Expand

If this error appears when adding a player from the **Provision** screen, the player already has an existing provisioning record under another BSN.Cloud network.

<p align="center">
    ![image-20240321-200712](https://github.com/user-attachments/assets/c9aa15bd-d1d2-475c-ba3b-05df3e3e0125)
</p>

A player can only have one provisioning record in BSN.Cloud, so the player’s existing provisioning record must be deleted and the player removed from its current network. To do this, follow the steps outlined [here](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/395313614/Provision#Deleting-a-Provision-Record). Only the owner of the network to which the player belongs can perform these functions so you may have to contact that person to request that they do this.

> [!INFO]
> Note that a factory reset of the player resets the settings of the player to its factory defaults but does **not** delete the player’s provisioning record. More info about that [here](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1936916598/Factory+Reset+a+Player).

#### How much do BSN.Cloud and BrightAuthor:connected cost?

![](https://brightsign.atlassian.net/wiki/images/icons/grey_arrow_down.png)

Expand

BrightAuthor:connected is free to use, just like BrightAuthor, and the Control Cloud tier is free on all connected players. The full feature set of Content Cloud is the same price as a BrightSign Network subscription, $99 per player per year.

#### Why did BrightSign create BSN.Cloud and BrightAuthor:connected?

![](https://brightsign.atlassian.net/wiki/images/icons/grey_arrow_down.png)

Expand

These were built to address many pain-points that BrightSign and our CMS partners faced in BrightAuthor and BrightSignNetwork, our legacy software. We simplified device deployment, network and player management, and delivered remote diagnostics, and made this functionality available to everyone. In addition, by using a more modern architecture, we’re able to provide a unified experience for BrightSign products on Mac and Windows, as well as through a Chrome web browser.

#### How do you secure my data in BSN.Cloud and BrightAuthor:connected?

![](https://brightsign.atlassian.net/wiki/images/icons/grey_arrow_down.png)

Expand

See our [security documentation](https://docs.brightsign.biz/display/DOC/Security) for BSN.Cloud and BrightAuthor:connected.

#### Should I use the desktop app (BrightAuthor:connected) or the web app (accessible at bsn.cloud)?

![](https://brightsign.atlassian.net/wiki/images/icons/grey_arrow_down.png)

Expand

BrightAuthor:connected, available for Mac or PC, is recommended for the vast majority of users. While much of the same functionality is available through both apps, the web app has some important limitations. The web app requires an internet connection and cannot access players through the user's local network (players must be connected to the internet). In addition, files must first be uploaded to BSN.Cloud before they can be used in presentations. BrightAuthor:connected does not have these limitations.

#### Can I use Dynamic Playlists without BSN.Cloud?

![](https://brightsign.atlassian.net/wiki/images/icons/grey_arrow_down.png)

Expand

No. A BSN.Cloud Content Cloud account is required to host Dynamic Playlists. However, you can get similar functionality with a self-hosted Media RSS (MRSS) feed, which can work with any player that has an internet connection. See [this FAQ](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/2308767745/Supported+Media+RSS+Feeds) for more details.

#### Can I get player usage statistics over BSN.Cloud?

![](https://brightsign.atlassian.net/wiki/images/icons/grey_arrow_down.png)

Expand

Yes, BSN.Cloud provides free, real-time access to basic health information and system diagnostics of connected players, including a visual representation of player status (via the [thermometer icon](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/415893546/Network+Status) on the Dashboard) and various types of [logging](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/384958995/Network#Logging). The log upload frequency can also be set.

All of these capabilities are available for both tiers of BSN.Cloud (the free Control Cloud tier as well as the subscription-based Content Cloud tier) and can be accessed with BrightAuthor:connected. Those in the Control Cloud tier can also use the web interface at control.bsn.cloud.

#### How long are log files stored if uploaded through BSN.Cloud?

![](https://brightsign.atlassian.net/wiki/images/icons/grey_arrow_down.png)

Expand

If you are using BSN.Cloud, and you enabled the **Upload Logs** feature in BrightAuthor:connected, log files will be deleted after they are successfully uploaded to BSN.Cloud. 

To enable **Upload Logs**:

1.  Go to the **Network** tab in BrightAuthor:connected
    
2.  Select your player.
    
3.  Go to **Properties > Logging** and select **Upload Logs.**
    

Log files that are more than 30 days old will automatically be deleted. If the player has no valid date and time, the maximum number of log files that will be stored is 60.

#### Can I update content, remotely and at the same time, on multiple players?

![](https://brightsign.atlassian.net/wiki/images/icons/grey_arrow_down.png)

Expand

Yes. BSN.Cloud allows you to organize your players into groups and schedule content to be deployed to one or more groups at the same time (or on different dates at different times). 

[Web Folder Setup](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1920434364/Web+Folder+Setup) allows multiple players to check the same folder on your remote web server for content updates. To update your players using this method, publish changes locally in BrightAuthor:connected, then transfer those changes to your web server. 

If you are using the BrightSign Network, you can organize your players into groups, and then schedule content to be deployed to one of more groups at the same time (or different times). [Simple File Network](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370671689/Simple+File+Network+Setup+in+BrightAuthor) in BrightAuthor lets you configure multiple units to check the same folder on your remote web server for content updates. To update your units, publish changes locally and then transfer those changes to your web server.

# Need More Help?

Try searching the [BrightSign FAQs](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1888813057/FAQs), or ask the [BrightSign community](http://support.brightsign.biz/hc/en-us/community/topics).

