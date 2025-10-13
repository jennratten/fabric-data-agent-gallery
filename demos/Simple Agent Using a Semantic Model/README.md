<h1><font size="6"><strong>Data Agents + Fast &amp; Simple</strong></font></h1>
<p>What if there was a way to build a Fabric Data Agent where it felt less like deciphering ancient hieroglyphics and more like ordering your favorite coffee?</p>
<p>Good news! With a little help from Copilot in Power BI, you can skip the guesswork, the endless documentation, the &ldquo;where did I save those notes?&rdquo; puzzle as well as the &ldquo;what&rsquo;s a schema?&rdquo; panic. Just ask Copilot eight smart questions, copy/paste the answers, and voil&agrave;&mdash;your agent is ready to roll. No code, no drama, just pure BI magic.</p>
<p>This guide is for anyone who likes speed, quality, and a little bit of tech wizardry. If you want to automate at scale, stay tuned for a future post!</p>
<h1><strong>Real-World Use Case</strong></h1>
<p>You have Power BI semantic models (datasets) in use today and want to create Fabric data agents for them, but you do not really know where to start, you keep getting stuck, or you want to work smarter, not harder. Perhaps the models are not documented or figuring out how to write the instructions is a challenge &ndash; or both. Copilot in Power BI to the rescue!</p>
<h1><strong>Scope</strong></h1>
<p>It is important to note that this method generates a &lsquo;general&rsquo; data agent in a low code / no code approach where the source is a semantic model that was developed using modeling best practices and is AI-Ready. Not to worry though, I will be writing about all kinds of variants&hellip; more on this later.</p>
<h1><strong>Before You Start</strong></h1>
<p>Before you can use these features, make sure you satisfy the requirements for the use of Copilot and Fabric data agents. You will also need a Power BI semantic model. I have included a <a href="https://github.com/jennratten/fabric-data-agent-gallery/tree/main/demos/Simple%20Agent%20Using%20a%20Semantic%20Model" target="_self">Git repo</a> with the files referenced in this post to make it easy for everyone to follow along. Microsoft also provides many sample reports that you can use to get familiar with Power BI - see this page: <a href="https://learn.microsoft.com/en-us/power-bi/create-reports/sample-datasets" target="_blank" rel="noopener">What are Power BI samples?</a>&nbsp;</p>
<h1><strong>Process at a Glance</strong></h1>
<p><li-image width="637" height="331" alt="jennratten_1-1760329274116.png" align="inline" id="1303124iED27C39F3583F576" size="large" resized="true" sourceType="new"></li-image></p>
<h1><strong>The Semantic Model</strong></h1>
<p>The semantic model is a standard star schema. For more info on star schemas see:&nbsp;<a href="https://learn.microsoft.com/en-us/power-bi/guidance/star-schema" target="_self">Understand star schema and the importance for Power BI</a></p>
<ul>
<li>Explicit measures are defined in a dedicated table named _Measures.</li>
<li>The Sales table is the fact table and is hidden.</li>
<li>Dimension/lookup tables have a one-to-many, single direction relationship with the Sales table.</li>
<li>Automatic aggregations are not enabled on any columns.</li>
<li>Hierarchies are present on some dimension/lookup tables.</li>
<li>Tables, columns and measures have user-friendly, logical names.</li>
<li>The Dates table has an active relationship with Order Date and an inactive relationship with Ship Date.</li>
</ul>
<p class="lia-indent-padding-left-30px"><font color="#000000"><li-image width="400" height="400" alt="jennratten_1-1760240133622.png" align="inline" id="1302995iB9E7A57250B66303" size="medium" resized="false" sourceType="new"></li-image></font></p>
<p class="lia-indent-padding-left-30px">&nbsp;</p>
<h1><strong>Chat with Copilot in a Power BI Report</strong></h1>
<p>Open a Power BI report in either the Power BI Desktop application or on the web, open the Copilot pane and send each of the messages below in the chat. I have tried several variations on these messages which I will be writing about in a future post.</p>
<ul>
<li>Gather all the information about the model that we want to provide to the data agent into the conversation.</li>
<li>Use the conversation to generate the inputs to configure the data agent.</li>
<li>Write test cases for the data agent and provide us with the expected answers.</li>
</ul>
<hr />
<p><strong><li-emoji src="/html/@DA3130730F54FC763C1178CDDBCD3FBA/emoticons/1f4a1.png" class="lia-deferred-image lia-image-emoji" id="lia_light-bulb" title=":light_bulb:"></li-emoji> PRO TIPS:</strong> <br />- The order matters. I experimented with several variations and got the best results with this set and order.<br />- Copy/paste and send a few items at a time; the Power BI Copilot chat allows up to 500 characters so you can knock these out with about 5 copy/paste rounds. This can go even faster by enabling your clipboard to hold multiple items (think clip-clip-clip, paste-paste-paste!) Check out <a href="https://www.howtogeek.com/671222/how-to-enable-and-use-clipboard-history-on-windows-10/" target="_self">these instructions for Windows 10</a>.&nbsp;<br />- Don't worry about copying any of the responses from Copilot until after you have sent all messages.<br />- Read the explanation of each item's value at the end of this post.</p>
<hr />
<p><li-image width="999" height="999" alt="jennratten_2-1760330502622.png" align="inline" id="1303125iCB09E07F17D663A2" size="large" resized="false" sourceType="new"></li-image></p>
<h2><strong>Messages to Send to Copilot</strong></h2>
<ol>
<li>Describe the structure of the dataset.</li>
<li>List the dataset schema.</li>
<li>Are any parts of the schema unused by the report?</li>
<li>List the data's explicit measures and calculations.</li>
<li>Explain how each explicit measure is defined and used.</li>
<li>List all relationships between tables, including cardinality and filter direction.</li>
<li>Provide all hierarchies and role-playing dimensions (e.g., Date roles like Order Date, Ship Date).</li>
<li>Using the model&rsquo;s metadata, list synonyms (terms), alternative names and properties for entities, measures, columns, and business terms.</li>
<li>Identify any calculation groups or time-intelligence patterns (e.g., YoY, MoM).</li>
<li>Specify grain constraints for measures (e.g., daily vs monthly validity).</li>
<li>Provide performance considerations (e.g., large tables, avoid certain joins, preferred filters).</li>
<li>List common business questions and their expected measures/dimensions.</li>
<li>Provide any denylist or whitelist for tables/columns beyond unused schema parts.</li>
<li>Include narrative guidance for KPIs (e.g., how to explain margin changes or discount impact).</li>
<li>Write detailed AI data agent instructions using the information provided in this conversation. Use as many details as possible, up to 15000 characters with all Markdown syntax (hashes for headings, double asterisks for bold, hyphens for lists, etc.) shown as plain text for copy/paste into another editor or system. Add these three sections at the beginning:<br /><strong>## 1. Task:</strong><br /><strong>## 2. Output Requirements:</strong><br /><strong>## 3. Mandatory Rules:</strong></li>
<li>Write 2-3 sentences to describe this data agent that will be displayed in &ldquo;About&rdquo; info to users.</li>
<li>Write 2-3 sentences to provide context when the agent appears in other experiences and for automated systems to use when deciding whether to use this agent.</li>
<li>Write 5-10 test cases for a Fabric data agent connected to the semantic model. The test cases MUST only include scenarios that align to the functionality of the Fabric data agent. When the expected response for a given test case does not vary based on a user's selection, include the value(s) expected instead of a reference of how to find them. Order the test cases by least complex to most complex.</li>
</ol>
<h1><strong>Create the Fabric Data Agent</strong></h1>
<p>Add a new item to your workspace and choose Data agent (preview) and give your agent a descriptive name (e.g., &ldquo;Retail Office Supplies Agent Demo&rdquo;).</p>
<p><li-image width="580" height="61" alt="jennratten_3-1760330910143.png" align="inline" id="1303126iC88CDA4B1E929988" size="large" resized="true" sourceType="new"></li-image></p>
<p><li-image width="584" height="238" alt="jennratten_4-1760330984247.png" align="inline" id="1303127i7E4BB1C64124A612" size="large" resized="true" sourceType="new"></li-image></p>
<h1><strong>Add a Data Source</strong></h1>
<p>Choose your semantic model and select the tables the agent should utilize. Select all tables to follow along with the demo.</p>
<p><li-image width="400" height="400" alt="jennratten_0-1760331121953.png" align="inline" id="1303128i7BBC37008258E127" size="medium" resized="false" sourceType="new"></li-image></p>
<h1><strong>Agent Instructions</strong></h1>
<p>Copy the response for item 15 (detailed instructions) and paste it into the agent&rsquo;s instructions.</p>
<p><li-image width="999" height="999" alt="jennratten_2-1760331935673.png" align="inline" id="1303130i4B1ABBE81E307E38" size="large" resized="false" sourceType="new"></li-image></p>
<p><li-image width="999" height="999" alt="jennratten_3-1760332149997.png" align="inline" id="1303132i523FB9CDEED0A4E7" size="large" resized="false" sourceType="new"></li-image></p>
<h1><strong>Agent Description that is Visible to Users in Fabric/Power BI</strong></h1>
<p>Open agent settings and add the About &gt; Description. Paste the response for item 16.</p>
<p><li-image width="999" height="999" alt="jennratten_4-1760332321473.png" align="inline" id="1303133i72638011850519DC" size="large" resized="false" sourceType="new"></li-image></p>
<h1><strong>Time to Test</strong></h1>
<p>Copy a test case from the response to item 18, paste it into the data agent chat, and send.&nbsp;Start with simple queries and increase complexity.</p>
<p><li-image width="999" height="999" alt="jennratten_0-1760332948860.png" align="inline" id="1303134i31E0BB5FFF5F2FFC" size="large" resized="false" sourceType="new"></li-image></p>
<hr />
<p><strong><li-emoji src="/html/@DA3130730F54FC763C1178CDDBCD3FBA/emoticons/1f4a1.png" class="lia-deferred-image lia-image-emoji" id="lia_light-bulb" title=":light_bulb:"></li-emoji> PRO TIP:</strong> The first couple of messages may take longer while your agent &ldquo;warms-up&rdquo;. The second time the question was asked, response time was cut in half.</p>
<hr />
<p>A lot of factors impact the response time (e.g. complexity of the question). This post oversimplifies for the sake of brevity. Look at out for a future post on this topic.</p>
<p><li-image width="999" height="999" alt="jennratten_0-1760334734858.png" align="inline" id="1303138i0E21BF67936E51A9" size="large" resized="false" sourceType="new"></li-image></p>
<h1><strong>Publish the Agent</strong></h1>
<p>When you are satisfied with the test results go ahead and publish the agent.</p>
<p>The description added here is what will be visible to automated processes and in external systems.&nbsp;After the agent is published this desciption can be accessed from the agent settings as well.</p>
<p><li-image width="999" height="999" alt="jennratten_1-1760335343589.png" align="inline" id="1303139i435B5A0DEF9C836A" size="large" resized="false" sourceType="new"></li-image></p>
<h1><strong>Test the Agent in the Standalone Copilot Experience in Power BI</strong></h1>
<p>This step is not essential but I highly recommend it, so you can test the agent from the user&rsquo;s perspective&hellip; see what your users will see.</p>
<p><li-image width="999" height="999" alt="jennratten_0-1760336011773.png" align="inline" id="1303140i5EF31830F7E94678" size="large" resized="false" sourceType="new"></li-image></p>
<p><li-image width="999" height="999" alt="jennratten_1-1760336078541.png" align="inline" id="1303141iB7242E473E3E3B52" size="large" resized="false" sourceType="new"></li-image></p>
<p><li-image width="999" height="999" alt="jennratten_2-1760336367555.png" align="inline" id="1303142iED13A84357E6B541" size="large" resized="false" sourceType="new"></li-image></p>
<p><li-image width="999" height="999" alt="jennratten_3-1760336385181.png" align="inline" id="1303143iF04286B2E609FF43" size="large" resized="false" sourceType="new"></li-image></p>
<p><li-image width="999" height="999" alt="jennratten_4-1760336403180.png" align="inline" id="1303144i7E0D9433672946F0" size="large" resized="false" sourceType="new"></li-image></p>
<h1><strong>Share the Agent</strong></h1>
<p>Now it&rsquo;s time to wow others with your awesome data agent! <br />Head back to the workspace and choose who to share it with and what permissions they should have. More on sharing an permissions here: <a href="https://learn.microsoft.com/en-us/fabric/data-science/data-agent-sharing" target="_self">Fabric data agent sharing and permission management (preview)</a><br /><br /></p>
<p><li-image width="999" height="999" alt="jennratten_5-1760336946218.png" align="inline" id="1303147i06FBC8482179A590" size="large" resized="false" sourceType="new"></li-image></p>
<p class="lia-indent-padding-left-150px"><li-image width="741" height="551" alt="jennratten_6-1760337008783.png" align="inline" id="1303150i2A5E67598C3B09D2" size="large" resized="true" sourceType="new"></li-image></p>
<h1><strong>Grant Build Permission on the Semantic Model</strong></h1>
<p>You&rsquo;re in the driver&rsquo;s seat with your Fabric data agent&mdash;just remember, when you share it, you also need to make sure the users can also access the underlying data. The agent strictly adheres to the underlying data&rsquo;s Row-Level Security (RLS) and Column-Level Security (CLS).&nbsp;Interacting with the data agent essentially equates to executing custom queries on-demand, that means build permission is your golden ticket. Learn how to grant build permission on the model here:&nbsp;<a href="https://learn.microsoft.com/en-us/power-bi/connect-data/service-datasets-build-permissions" target="_self">Build Permission for Shared Semantic Models</a></p>
<hr />
<p><strong><li-emoji src="/html/@DA3130730F54FC763C1178CDDBCD3FBA/emoticons/1f4a1.png" class="lia-deferred-image lia-image-emoji" id="lia_light-bulb" title=":light_bulb:"></li-emoji> PRO TIP:</strong> If you have already shared the model&rsquo;s reports with users through a Power BI App...<br />&nbsp; &nbsp; &bull; First&hellip; <strong>GOLD STAR</strong> to you for using a best practice!<br />&nbsp; &nbsp; &bull; Second&hellip; you can go back into the app configurations &gt; audience and tick the box to allow the users to build with models used by the app. This will grant build permission to everyone in your audience in one click. If more than one model is referenced in the app for the audience, users get build access for all of them. Read more about Power BI apps here: <a href="https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-create-distribute-apps" target="_self">Publish an app in Power BI</a></p>
<hr />
<p><li-image width="400" height="400" alt="jennratten_0-1760337642685.png" align="inline" id="1303152i0598025C6AB29D24" size="medium" resized="false" sourceType="new"></li-image></p>
<h1><strong>Why This Works</strong></h1>
<p>&bull; Copilot Knows Your Stuff: It instantly understands your semantic model&mdash;structure, measures, relationships, and all.<br />&bull; AI-Ready Models = Happy Copilot: Clean names, curated measures, and no unused clutter mean Copilot delivers spot-on instructions and test cases.&nbsp;<br />&bull; No More Manual Documentation: Forget digging through endless fields and writing instructions from scratch.<br />&bull; Reusable Framework: This simple method has been tested and worked successfully on 6 semantic models of different content and subjects. Deploy agents like a pro!</p>
<h1><strong>Items in Preview Can Change Without Notice</strong></h1>
<p>It is also important to note that the Fabric data agent item is till in preview, meaning the way it works and documentation surrounding it may change or be something other than expected during the preview period. The differences that I noticed were mainly involving the data agent item&rsquo;s instructions in the Fabric workspace. For example, during the time spent writing this post, the agent instructions input has changed from plain text to markdown and its location has changed from appearing to the right of the chat to the left of the chat.&nbsp;Read more about the expectations here: <a href="https://learn.microsoft.com/en-us/fabric/data-science/how-to-create-data-agent" target="_self">Create a Fabric data agent (preview)</a></p>
<h1><strong>Ready to launch your first Fabric Data Agent in record time?</strong></h1>
<p>With these simple steps, you&rsquo;re not just building agents&mdash;you&rsquo;re putting production-ready solutions in place almost as fast as you can say &ldquo;no code required.&rdquo; Whether you&rsquo;re a data rookie or a seasoned engineer, this approach lets you skip the guesswork and manual documentation. Stop over-engineering and over-thinking your agent. Open your report, send some messages, and let Copilot do the heavy lifting. You will wow your team in no time!</p>
<h1><strong>A Friendly Guide to Power BI and Fabric AI (Beginner to Expert)</strong></h1>
<p>This post is the first in a new series all about making Power BI and Fabric&rsquo;s AI features work for you&mdash;no matter your background or skill level. Whether you&rsquo;re a business user just getting started, a low-code developer looking for shortcuts, or a pro-code expert building advanced solutions, you&rsquo;ll find practical tips and clear examples you can use right away. We&rsquo;ll cover everything from using the built-in UI to creating scalable, custom solutions, all explained in a way that&rsquo;s easy to follow and act on. So, wherever you are on your data and AI journey, you&rsquo;re in the right place!</p>
<h1><strong>Links to Documentation</strong></h1>
<p><a href="https://learn.microsoft.com/en-us/power-bi/create-reports/tutorial-copilot-power-bi-introduction" target="_blank" rel="noopener">Copilot in Power BI tutorial introduction</a><br /><a href="https://learn.microsoft.com/en-us/power-bi/create-reports/copilot-reports-overview" target="_self">Use Copilot with Power BI reports and semantic models</a><br /><a href="https://learn.microsoft.com/en-us/fabric/data-science/how-to-create-data-agent" target="_self">Create a Fabric data agent (preview)</a><br /><a href="https://learn.microsoft.com/en-us/fabric/data-science/data-agent-copilot-powerbi" target="_self">Consume a Fabric Data Agent from Copilot in Power BI (preview)</a><br /><a href="https://learn.microsoft.com/en-us/fabric/data-science/data-agent-tenant-settings" target="_self">Fabric data agent tenant settings</a><br /><a href="https://learn.microsoft.com/en-us/fabric/data-science/data-agent-sharing" target="_self">Fabric data agent sharing &amp; versioning</a><br /><a href="https://learn.microsoft.com/en-us/power-bi/create-reports/copilot-chat-with-data-standalone" target="_self">Standalone Copilot experience in Power BI (preview)</a><br /><a href="https://learn.microsoft.com/en-us/power-bi/create-reports/copilot-enable-power-bi" target="_self">Enable Fabric Copilot for Power BI (tenant)</a><br /><a href="https://learn.microsoft.com/en-us/power-bi/guidance/star-schema" target="_self">Understand star schema and the importance for Power BI</a><br /><a href="https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-create-distribute-apps" target="_self">Publish an app in Power BI</a><br /><a href="https://learn.microsoft.com/en-us/power-bi/connect-data/service-datasets-build-permissions" target="_self">Build Permission for Shared Semantic Models</a></p>
