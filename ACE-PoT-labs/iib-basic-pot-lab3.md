---
title: Using Patterns to Work with Files
toc: false
sidebar: labs_sidebar
folder: pots/iib-basic
permalink: /iib-basic-pot-lab3.html
summary: Moving files through IIB
applies_to: [developer]
---

# Lab 3 Using Patterns to Work with Files

In this lab will you will learn how to start from, configure, and instantiate a pattern. You will also implement file processing, content-based routing, and file-to-HTTP protocol switching. The lab implementation reads JSON files, routes them based upon the value of a *country* field, and calls an HTTP web service that is provided by a Node.js application.

You will use an integration node named **POTNODE** and an integration server named **default**.

## Selecting and Configuring the Filesystem Location

In this section you will select and configure a filesystem location that IIB will read files from.  If you are using the PoT image the following steps have already been performed, but you should read the steps so you are familiar with IIB file processing.

1.  Create or select a directory where IIB will read input files and make a note of its path (e.g. **C:\\student10\\Lab3**). Under that path, create a subdirectory named **file\_to\_http\_sample** and, as a peer, another subdirectory named **out**.  (This has already been completed on the PoT image.)

2.  Set the **MQSI\_FILENODES\_ROOT\_DIRECTORY** environment variable to the path in the prior step. For example, on Windows, navigate to **Control Panel/All Control Panel Items/System**, click on **Advanced system settings**, then **Environment Variables**, then set this variable as a system variable; then log out and log back in. (This has already been completed on the PoT image.)
	
	![](/lab3-images/FileRootEnvVar.png)
    
    This environment variable sets the starting point for the relative file paths (e.g. *file\_to\_http\_sample*) used in this lab’s implementation.

## Preparing the IIB Toolkit Workspace

<span id="_Toc136939320" class="anchor"><span id="_Toc136943190" class="anchor"><span id="_Toc141180388" class="anchor"></span></span></span>In this section you will prepare an empty IIB Toolkit workspace with the pattern.

1.  Double-click on the desktop shortcut for the IIB V10 Toolkit. When prompted for a workspace, enter a path for an empty workspace then click **OK**.

    ![](/lab3-images/WorkspaceLauncher.png)

2.  Close the **Welcome** panel.

    ![](/lab3-images/CloseWelcome.png)

3.  In the Toolkit’s upper left, click on **Patterns Explorer** tab. Then select **Pattern Repositories/Experimental OT4I GitHub Pattern Repository/File Processing/Record Distribution/HTTP one-way**, opening the Pattern Specification editor for *Record Distribution to HTTP: one-way pattern*. The Patterns Explorer view should indicate that this pattern currently is not installed.

    ![](/lab3-images/PatternSpecification.png)

4.  In the lower right of the Pattern Specification editor, click on **Download and Install**.

    ![](/lab3-images/DownloadInstall.png)

5.  Let the download complete. If prompted with a security warning, click **OK** to proceed. Upon completion of the download, the Patterns Explorer should indicate that the HTTP one-way pattern is now installed.

    ![](/lab3-images/PatternInstalled.png)

6.  Read all of the information on the Pattern Specification view for this pattern, including the links in the Message Flows and Related Tasks sections.


## Configuring and Generating the Pattern Instance

1.  In the **Patterns Explorer**, select **Patterns/File Processing/Record Distribution/HTTP one-way** and single-click.  (NOTICE: The correct path is under the **Patterns** folder, not the sibling folder named **Pattern Repositories**.)

	 ![](/lab3-images/PatternsHTTPOneWay.png)

3.  On the resulting **Pattern Specification** page, click **Create New Instance**. 

    ![](/lab3-images/CreateNewInstance.png)

2.  On the New Pattern Instance panel, enter **Lab3** for the name then click **OK**.

    ![](/lab3-images/NamePatternInstance.png)

3.  On the **Pattern Configuration** editor, specify exactly the values shown in the screen capture below. Then click **Generate** in the lower left of the panel and let pattern generation complete.

    ![](/lab3-images/PatternConfiguration.png)

4.  Select **Window->Reset Perspective**. On the Reset Perspective panel, click **Yes**.

    ![](/lab3-images/ResetPerspective.png)

1. As mentioned in the Solution section of the above Pattern Specification, use of this pattern requires installation of the **Node.js** runtime, this has already been performed on the PoT image. 
 
	If you are not using the PoT image and your system does not have Node.js installed, follow the instructions in Appendix A of this document to install the Node.js runtime. When the Node.js installation has been successfully completed continue with the next step.

1. Open a command prompt to the current workspace for the IIB Toolkit (e.g. **C:\\student10\\workspaces\\Lab3**) and navigate to **Lab3_HTTP-oneway\_sample/webserver**. From there, run the **start\_server.&lt;ext&gt;** script appropriate for your platform; for example, **start\_server.bat** on the PoT image. The first time you run the command, you will see the messages preceded with dashes in the screen capture below. The **Listening on port 3000** message indicates that the web service is up and ready.

    ![](/lab3-images/StartNodeWebService.png)
	
## Running the Generated IIB Application

1.  In the Application Development view, expand the **Lab3\_HTTP one-way** Application, select the **RecordDistributor** message flow, and double-click to open it in a message flow editor. Review the flow, its nodes, their settings, and the Pattern Specification to ensure that you understand what this flow does: reads JSON files from the **C:\student10\Labs\file\_to\_http\_sample** directory, parses them as JSON, routes them based upon the country specified in the JSON, and submits an HTTP request to the URL appropriate for that country.

2.  With the **RecordDistributor** message flow still open in a message flow editor, click the red **Flow Exerciser** button. If the toolkit presents a *Ready to record message* panel, check the box for *Do not show this message again* then click **Close**.

    ![](/lab3-images/StartFlowExerciser.png)

    The Application should be deployed, and flow recording should start.

3.  In the Integration Nodes view in the Toolkit’s lower left, confirm that the **Lab3\_HTTP one-way** Application deployed.  

    ![](/lab3-images/Deployed.png)

4.  Run the flow. In the Application Development view, navigate to **Independent Resources/Lab3\_HTTP-oneway\_sample** and select the **Record1.json** file. Right-click then select **Copy** to copy the file. Paste the file into the **C:\student10\Lab3\file\_to\_http\_sample** directory polled by the flow’s File Input node. The RecordDistributor flow will read the file, route it based upon the **country** value in the JSON, and send the request to the corresponding URL.

5.  Confirm that the web service has received the request sent by the IIB flow. Look in the Node.js start\_server window for the **Record Saved** message shown below.

    ![](/lab3-images/UnitedKingdom.png)

    This output indicates successful execution of the message flow.

6.  Examine the path that the file data took through the message flow. At the top of the message flow editor for the RecordDistributor flow, click the **View Path** icon.

    ![](/lab3-images/ViewPath.png)

    Green highlighting will appear to indicate the path the previous file data took through the flow. Click on the **envelope icon** on the wire between the File Input and Record Processor nodes.

    ![](/lab3-images/EnvelopeIcon.png)

    View the message data in the Recorded Message dialog. In particular, notice the value of the *country* field.

    ![](/lab3-images/RecordedMessageUK.png)

    Click the **envelope icon** on the green wire between the Route node and the HTTP Request 0 node. View the data in the new Recorded Message dialog. The Route subflow routed the message through this path of the flow based upon the value of the *country* field.

7.  Rerun the RecordDistributor flow with different files. Repeat the prior three steps using the files **Record2.json** and **Record3.json**. Because each of these files has a different country value, they will take different paths through the flow.

# Summary
-------

This lab has provided an illustration of how to start from, configure, and instantiate a pattern. It has also illustrated file processing, content-based routing, and file-to-HTTP protocol switching.

# Appendix A: Installing a Node.js Runtime
----------------------------------------

A Node.js application acts as the web service provider for this lab and requires a Node.js runtime installation, follow the instructions in this section to install the Node.js runtime.

1.  Use a browser to navigate to <http://nodejs.org>.

2.  From there, click the link to download the Node.js installer for your operating system. 

3.  Upon completion of the download, run the installer.

4.  As shown on the Node.js panel below, choose to do a complete installation of Node.js.

	![](/lab3-images/NodejsSetup.png)

5.  Follow the remaining panels to complete installation of the Node.js runtime. Upon completion, click **Finish** in the panel below.

    ![](/lab3-images/NodejsSetupFinish.png)
