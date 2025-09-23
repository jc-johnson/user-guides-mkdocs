# How to Add Paragraph Spacing Inside of Notes in Madcap Flare

## Context

Notes are a great way of highlighting important information in MadCap Flare. Some notes require long blocks of text that are better broken up yet still contained within the same note block. 

## Process

To create spacing within a note in MadCap Flare follow the following steps:

1. Create a custom div style for notes.
2. Create separate divs nested inside of the note div to separate content. 

The best way to create spacing between paragraphs within the same note in MadCap flare is to create separate divs of content nested inside the parent note div. You can do this easily using the XML editor in MadCap Flare.

Between each separate block of text also add a div that simply adds a space between paragraphs of text. 

## Creating a Note DIV Style

To create styling for content that should be inside of a note, you have to create a custom class in your stylesheet in your MadCap Flare project. Complete the following steps: 

1. In MadCap Flare in the Content Explorer, navigate to **Resources > Stylesheets > [Your Project Stylesheet].css**
2. Right click the CSS file and select Open with > Internal Text Editor  
3. Add a definition for the CSS properties for div.note content similar to the example below.
4. Save the changes you made to the stylesheet. 

In a project topic, select the content you want to put inside of a note and select the newly created div.note style from the style dropdown in the Styles window on the Home tab. 

Separating Content Within a Note

1. Right-click on your topic in the MadCap Flare File Explorer.
2. Edit your topic using the Text Editor. 
3. Insert a code snippet similar to the code sample below. 

**Note:** Use the following line to create spacing between paragraphs within the note div: **<div>&#160;</div>**

## Code sample

## Result

The note from the above code will appear as follows: