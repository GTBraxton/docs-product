---
tags: runtime-traditionalweb; 
summary: Wizard splits complex tasks and process into steps.
---

# Wizard 

<div class="info" markdown="1">

We’ve been working on this article. Please let us know how useful this new version is by voting.

</div>

You can use the Wizard UI Pattern to split large complex tasks and processes into smaller manageable steps. A wizard presents a series of steps or conditions that the user needs to complete in order to accomplish a goal. Additionally, wizards usually include explicit button navigation to move a step forward or backward. Some wizard examples include software installation wizards and sign-up screens.

![](<images/wizard-24-ss.png>)

**How to use the Wizard UI Pattern**

The following example demonstrates how you can create a four step Wizard with navigation buttons. The example is made up of the following steps:

* Creating a wizard
* Adding content to the wizard
* Creating the wizard navigation

**Create a wizard**

1. In Service Studio, in the Toolbox, search for `Wizard`.

    The Wizard and Wizard Item widgets are displayed (both of which are required to use this pattern).

    ![](<images/wizard-23-ss.png>)

    If the UI widget doesn't display, it's because the dependency isn't added. For example, if you are using a ready-made app, it deletes unused widgets from the module. To make the widget available in your app:

    1. In the Toolbox, click **Search in other modules**.

    1. In **Search in other Modules**, remove any spaces between words in your search text.
    
    1. Select the widget you want to add from the **OutSystemsUIWeb** module, and click **Add Dependency**. 
    
    1. In the Toolbox, search for the widget again.

1. From the Toolbox, drag the Wizard widget into the Main Content area of your application's screen.

    ![](<images/wizard-1-ss.png>)

    By default, the Wizard widget contains three Wizard Item widgets. Each Wizard Item represents a step. You can add or delete Wizard Items as required.

1. From the Toolbox, drag another Wizard Item into your Wizard Pattern. 

    ![](images/wizard-28-ss.png)

1. Enter `4` for the new Wizard Item icon.

    ![](images/wizard-27-ss.png)

1. Rename each of the Wizard Items to the following:

    * Shopping Details
    * Payment Details
    * Review Order
    * Confirm Order

    ![](images/wizard-20-ss.png)

1. From the Element tree, create an Input Parameter by right-clicking on your screen, and from the drop-down, select **Add Input Parameter**.

    The input parameter controls which Wizard step is shown to the user.

    ![](images/wizard-25-ss.png)

1. On the **Properties** tab, set the Input Parameter properties as follows:

    * Name: CurrentStep
    * Data Type: Integer
    * Is Mandatory: No
    * Default Value: 1

    ![](images/wizard-13-ss.png)

     By setting the **Default Value** to 1, you ensure that the  Wizard always starts on step 1.

1. To create the logic that defines the status of each Wizard Item (as an active step, a past step, or a next step), select the first Wizard Item (step 1), and on the **Properties** tab, from the **Step** drop-down, select **Expression Editor**.

    ![](images/wizard-29-ss.png)

1. In the expression editor, enter the following expression:

    `If(CurrentStep = 1, Entities.Step.Active,If(CurrentStep > 1, Entities.Step.Past, Entities.Step.Next))`

    ![](images/wizard-19-ss.png)

    This logic has the following meaning:

    * If the user is on step 1, the step is displayed as the active step in the wizard.
    * If the user is on a step greater than step 1, step 1 is displayed as a step that is in the past (completed).
    * If the user is on a step less than 1, the step is displayed as an upcoming (next) step.

1. Repeat steps 8 and 9 for all of the Wizard Items. Replace the number 1 in the expression with 2, 3, and 4 respectively.

**Add content to the wizard**

1. From the Toolbox, drag the If widget onto the main content area of your application's screen, just below the Wizard Pattern.

    ![](images/wizard-30-ss.png)

1. On the **Properties** tab, in the **Condition** property, enter the following:

    `CurrentStep = 1`

    ![](images/wizard-19-ss.png)

    You have now created a condition that controls what's displayed on screen when the step is active.

1. Repeat steps 1 and 2 for all of the Wizard Items. Replace the **Condition** property with 2, 3, and 4 respectively.

1. In the top section (True) of the If widgets, create the relevant content for each of the steps.

    The following example shows a Shipping Details step that contains labels and input boxes.

    ![](images/wizard-18-ss.png)

**Create the wizard navigation**

1. From the Toolbox, drag two Button widgets onto your screen.

1. On the **Properties** tab, define the button names and the button behavior (previous and next).

    | Property | Button 1 | Button 2
    |---|---|---|
    | Label | "Previous" | "Next" |
    | Method | Navigate/Submit | Navigate/Submit |

1. To ensure that all of the information the user enters is passed from step to step, create a [screen action](../../../../logic/action-web.md#screen-actions) by selecting the **Next** button.

1. On the **Properties** tab, from the **Destination** drop-down, select **New Screen Action**.

    ![](images/wizard-22-ss.png)

1. From the Toolbox, drag the Assign block onto your screen and set the **Variable** property to `CurrentStep` and the **Value** property to `CurrentStep + 1`. This ensures that user inputs are passed from step to step.

    ![](images/wizard-21-ss.png)

1. Repeat steps 4 and 5 for the **Previous** button, setting the **Variable** property to `CurrentStep` and the **Value** property to `CurrentStep - 1`.


1. To display the **Next** button when applicable, select the **Next** button, right-click, and select **Enclose in If**.

    ![](images/wizard-26-ss.png)

1. On the **Properties** tab, in the **Condition** property, enter the following:

    `CurrentStep < 4`

    ![](images/wizard-17-ss.png)

    You have now created a condition that ensures that the user can never go above the number of steps in the wizard.

1. Repeat steps 7 and 8 for the **Previous** button. Enter `CurrentStep > 1` as the **Condition** property. This ensures the **Previous** button is only displayed when applicable, and the user can never go below the number of steps in the wizard.

After following all of the steps in each of the sections, you can publish the module, and test the Wizard in your app.

## Properties

### Wizard

| Property |  Description |
|---|---|
| Orientation (Orientation Identifier): Optional  | <p>Set the wizard orientation. By default the Wizard displays horizontally.</p><p> Examples <ul><li>_Entities.Orientation.Horizontal_ - The wizard displays horizontally.</li><li>_Entities.Orientation.Vertical_ - The wizard displays vertically.</li></ul></p>|
| ExtendedClass (Text): Optional  | <p>Adds custom style classes to the Pattern. You define your custom style classes in your application using CSS.</p> <p>Examples <ul><li>_Blank_ - No custom styles are added. This is the default.</li><li>_''myclass''_ - adds the _myclass_ style to the UI styles being applied</li><li>_''myclass1'' ''myclass2''_ - Adds the _myclass1_ and _myclass2_ styles to the UI styles being applied.</li></ul></p>You can also use the classes available on the OutSystems UI. For more information, see the [OutSystems UI Live Style Guide](https://outsystemsui.outsystems.com/StyleGuidePreview/Styles). |

### Wizard Item

| Property |  Description |
|---|---|
| Step (Step Identifier): Mandatory | <p>Set the status of the Wizard Item relative to the current step of the Wizard. You can customize an expression to set the status of the Wizard Item or you can use the predefined values Active, Next, and Past. </p><p>Examples <ul><li>_Extended.Step.Active_ - Sets the Wizard Item to active, that is, the current step the user is on.</li><li>_Extended.Step.Next_ - Sets the Wizard Item to incomplete, that is, a step that is yet to be completed by the user.</li><li>_Extended.Step.Past_ - Sets the step to inactive, that is, a step that has already been completed by the user.</li></ul></p>| 
| UseTopLabel (Boolean): Optional  | If True, label is placed above the icon. If False, label is placed below the icon. The text describing the step is either placed above or below the step icon. | 
| ExtendedClass (Text): Optional | <p>Adds custom style classes to the Pattern. You define your custom style classes in your application using CSS.</p> <p>Examples <ul><li>_Blank_ - No custom styles are added. This is the default.</li><li>_''myclass''_ - Adds the myclass style to the UI styles being applied.</li><li>_''myclass1'' ''myclass2''_ - Adds the _myclass1_ and _myclass2_ styles to the UI styles being applied.</li></ul></p>You can also use the classes available on the OutSystems UI. For more information, see the [OutSystems UI Live Style Guide](https://outsystemsui.outsystems.com/StyleGuidePreview/Styles). | 
