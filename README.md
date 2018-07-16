# GildedRose

Inventory application to manager your items in your warehouse 

## Getting Started

Please download the source code for this application by downloading the file **GildedRose.zip**
Or download the executable application (exe) by downloading the file **GildedRoseExecutable.zip**

### Prerequisites

*	C#.Net
*	Framework 4.5 or bigger 
*	Install Visual Studio 2012 or bigger 
*	XML editor (Ex. Notepad ++)

## Installing

If you download the source code from **GildedRose.zip**, please copy and paste the folder in your preferred location of your computer and open the solution in your Visual Studio.

If you download the executable from **GildedRoseExecutable.zip**, please copy and paste the folder in your preferred location of your computer and execute GildedRose.exe.

## Application configuration

Properties of each item 

*	All items have a SellIn value which denotes the number of days we have to sell the item
*	All items have a Quality value which denotes how valuable the item is
*	At the end of each day our system lowers both values for every item

### Items Rules 

The following rules can be applied to the items 

*	Once the sell by date has passed, Quality degrades twice as fast
*	The Quality of an item is never negative
*	Some items can increase the quality the older it gets
*	The quality of an item is never more than 50
*	Some items can be a legendary, never has to be sold or decreases in Quality
*	Some item could have more than one Rule that can be applied for the same item 
*	Some items can over pass 50 as quality 
*	Every item has rules 

### Configuration of the Application 

The application has been developed to create and update items base on the rule configuration of each item

Inside the folder application you will find a sub folder called DataBase inside you will find two xml documents, each xml document contains the configuration of the inventory. 

**XML Items**

This XML was created to have the list of items of your inventory.

The following configuration must be created by a user with stronger knowledge in XML structure.
Please go to “../DataBase/Items.Xml”

The following XML contains the structure to organize items 

```
<items>
  <item>
    <ItemId>+5 Dexterity Vest</ItemId>
    <SellIn>10</SellIn>
    <Quality>20</Quality>
    <ItemNum>1</ItemNum>
  </item>
</items>
```

Nodes…
*	ItemId = Name of the Item
*	SellIn = Limit day to be sell 
*	Quality = Quality of the item 
*	ItemNum = Item number unique, this value cannot be repeated 

**XML Items Rules**

This XML was created to have rules for each item.
The following structure was created to manage the item with multiples rules or only one rule.

The following configuration must be created by a user with stronger knowledge in XML structure.
 
- **Items with one Rules** -

The following XML contains the default Rule structure for the item 

```
<Rules>
  <RulesCategory>
    <!—Structure of the Default Rules - - >

    <ItemNum>1</ItemNum>
    <MinQuality>0</MinQuality>
    <MaxQuality>50</MaxQuality>
    <AfterSellIn>-2</AfterSellIn>
    <BeforeSellIn>-1</BeforeSellIn>
    <mutateQuality>true</mutateQuality>
    <mutateSellIn>true</mutateSellIn>
    <!— End Structure of the Default Rules - - >

  </RulesCategory>
</Rules>
```

Nodes…
*	ItemNum = Item number unique, this value is the relationship with itemNum in Items.xml
*	MinQuality = Minimum quality value for this item, value can not be less than cero 
*	MaxQuality = Maximum quality value for this item
*	AfterSellIn = Increase or decrease value in quality after the selling date is reach  
       
       **Important** = operation signs are important
       
			                *-4 = This number is negative 
			                * 4 = This number is positive 
                      
*	BeforeSellIn = Increase or decrease value in quality before the selling date is reach
       
       **Important** = operation signs are important
			                
                      *-4 = This number is negative 
			                * 4 = This number is positive 
                      
*	mutateQuality =  Only two values are accepted 
                    
                    *true = The Quality value will change 
                    *false = The Quality value wont change 

*	mutateSellIn =Only two values are accepted 

            *true = The SellIn value will change 
            *false = The SellIn value wont change 


 
- **Items with more than one Rules** -

The following XML contain the default rule structure for the item and one or more additional rules.
For this scenario the rules taken in consideration are the additional rules and not the default rules 

```
<Rules>
  <RulesCategory>

    <!—Structure of the Default Rules - - >
    <ItemNum>8</ItemNum>
    <MinQuality>0</MinQuality>
    <MaxQuality>50</MaxQuality>
    <AfterSellIn>0</AfterSellIn>
    <BeforeSellIn>1</BeforeSellIn>
    <mutateQuality>true</mutateQuality>
    <mutateSellIn>true</mutateSellIn>
    <!— End Structure of the Default Rules - - >

    <!- Begin of the Additional rules -- >
    <RulesItem>
      <Rule>
        <RuleId>1</RuleId>
        <MinQuality>0</MinQuality>
        <MaxQuality>50</MaxQuality>
        <LimitDays>10</LimitDays>
        <AfterSellIn>0</AfterSellIn>
        <BeforeSellIn>2</BeforeSellIn>
        <mutateQuality>true</mutateQuality>
        <mutateSellIn>true</mutateSellIn>
      </Rule>
      <Rule>
        <RuleId>2</RuleId>
        <MinQuality>0</MinQuality>
        <MaxQuality>50</MaxQuality>
        <LimitDays>5</LimitDays>
        <AfterSellIn>0</AfterSellIn>
        <BeforeSellIn>3</BeforeSellIn>
        <mutateQuality>true</mutateQuality>
        <mutateSellIn>true</mutateSellIn>
      </Rule>
      <Rule>
        <RuleId>3</RuleId>
        <MinQuality>0</MinQuality>
        <MaxQuality>50</MaxQuality>
        <LimitDays>0</LimitDays>
        <AfterSellIn>0</AfterSellIn>
        <BeforeSellIn>0</BeforeSellIn>
        <mutateQuality>true</mutateQuality>
        <mutateSellIn>true</mutateSellIn>
      </Rule>
    </RulesItem>
    <!- End of the Additional rules -- >

  </RulesCategory>
</Rules>
```
 
Nodes…
*	ItemNum = Item number unique, this value is the relationship with itemNum in Items.xml
*	MinQuality = Minimum quality value for this item, value cannot be less than cero 
*	MaxQuality = Maximum quality value for this item
*	AfterSellIn = Increase or decrease value in quality after the selling date is reach  
       
       **Important** = operation signs are important
			
                    *-4 = This number is negative 
			              * 4 = This number is positive 
*	BeforeSellIn = Increase or decrease value in quality before the selling date is reach
       
       **Important** = operation signs are important
       
			              *-4 = This number is negative 
			              * 4 = This number is positive 
                    
*	mutateQuality =  Only two values are accepted 

                    *true = The Quality value will change 
                    *false = The Quality value wont change 

*	mutateSellIn =Only two values are accepted 
    
                *true = The SellIn value will change 
                *false = The SellIn value wont change 
                
*	LimitDays = Limit Day to be executed, this value cannot be negative; this value applied only for additional rules 

          **Example**
	          
           Execution rule between 
                *0 day (before Sell In) and LimitDay
                  or 
                * 5 days (before Sell In) and LimitDay 

- **GildedRose.exe.config** -

App configuration file was creating to make the reference between the xml file name and the application.
If one of the XML file name change, the files name of the XML file needs to be change in the configuration of the application

```
<applicationSettings>
    <GildedRose.Properties.Settings>
      <setting name="ItemXml" serializeAs="String">
        <value>/DataBase/Items.xml</value>
      </setting>
      <setting name="ItemRulesXml" serializeAs="String">
        <value>/DataBase/ItemsRules.xml</value>
      </setting>
    </GildedRose.Properties.Settings>
  </applicationSettings>
```

**Settings**

*	ItemXml = If the value change; change the node value with the new XML Item.xml file name 
*	ItemRulesXml = If the value change; change the node value with the new XML ItemRulesXml.xml file name 
 
# User Guide 

This application was created to manage the items of your inventory allowing you to add or modified existent items and their Rules without modified the actual code.

The XML items.xml file will allow you to add or modified items base on your needs.
The XML ItemRules.xml file will allow you to add or modified the rules of the item base on the application rules previously discussed. 

Once the application is installed, the user only need to execute the application to see the result; the application can be executed by clicking “F5”, if you run it from Visual studio or by executing the .exe GildedRose.exe on your application folder.

The result can be found in Result.txt created at the level of the application folder 
*	From visual studio ../bin/[Debug/Release]
*	Application folder at root level 


## Limitations 

1.	The application is validated however the structure of the XML is not validate by the application. I highly recommend creating the configuration by a user with knowledge in XML structure.
2.	If the application Rules change, the application core will need to be modified by the development department. 

# Contributors

Eduardo Zertuche  

# License
V 1.0.0

