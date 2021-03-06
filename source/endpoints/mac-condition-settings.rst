Scan Condition Settings
=======================

You can scan macOS condition settings to include processes, files, system, and authenticated users

#. Go to **Policy** in the top panel
#. Go to **Policy > Node Policy > Agent Action** in the left Policy panel
#. Find and click **Scan Condition Settings** in the Agent Action window

Under **General** section

#. For **CWP Message**, add message to be displayed in accordance with the Policy
#. For **Label**, add labels to help categorize your plugins with custom labels that appear in the "Description" field

Under **Agent Actions** section (*Must have Conditions added for this plugin to work*)

#. For **Boolean Operator**, choose **AND** or **OR** to add optional conditions
#. For **Settings**, click **Add** and select your optional conditions. **Criteria/Operator/Value**
#. For **Execution Interval**, adjust Periodic Interval (*Seconds - months*) 
#. Enter in **Conditions**, and adjust **Execution Interval**
#. For **Periodic Interval**, choose from seconds, minutes, hours, days weeks, or months (*Default is 12 hours*)
#. Click **Update**
#. Go to **Node Policy** in the left Policy panel
#. Click the **Default Policy** in Node Policy window
#. Find **Agent Action**. Click **Assign**
#. Find **Scan Condition Settings** in the **Available** section. Select and drag it into the **Selected** section
#. Click **Add**
#. Click **Update**
