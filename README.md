# spRest
sharepoint rest manipulation
spRest v1.0b

ABSTRACT
spRest is a lightweight sharepoint lists communication library.
It contains 4 basic functions:

zGetItems
Returns an array of associative arrays, one for each list item.

	var list=zGetItems({listName:’listName’});


zNewItem
Create a new item based on values passed into function.

	zNewItem({listName:’list’,newItem:{Field1:’value1’,Field2:’value2’}});

zModifyItem
Modify one list item based on list item ID

	zModifyItem({listName:’list’,id:2});

zDeleteItem
Delete item(s) from the list based on item(s) id(s) passed in an array.

	zDeleteItem({listItem:’list’,id:[1]});
	zDeleteItem({listItem:’list’,id:[1,2]});


 
1.	zGetItems(parameter) - get all items from the list and parse them into an object
parameter [object]

	parameter [object]
		NAME		  |	MAN./OPT.	|	DEFAULT			  |	TYPE	  |	INFO										                  |	REMARKS
		listName	|	mandatory	|					      |	string	|												                    |
		url			  |	optional	|	current url		|	string	|												                    |
		async		  |	optional	|	true			    |	boolean	|	asynchronous call							            |
		expand		|	optional	|	none			    |	array	  |	used for lookup and person/group fields 	|	Field name must start with capital letter even if in the list it doesn't
		filter		|	optional	|	none			    |	object	|	used for filtered query /positive filter	|	Field name must start with capital letter even if in the list it doesn't
	

==EXAMPLE==
  zGetItems({
    listName: "name",
    url: "https://troom.capgemini.com/sites/testSite/",		//optional
    async: false,								//optional
    expand: ["CreatedBy","ModifiedBy"],					//[fieldName1, fieldName2,...]
    filter:{
      Name: "Mietek",							//field name: value
      Age: 18								//field name: value
    }
  });
 
2.	zNewItem(parameter) - create new list item in the list and with field values indicated in parameter
	parameter [object]

		NAME		  |	MAN./OPT.	|	DEFAULT			  |	TYPE	  |	INFO				      |	REMARKS
		listName	|	mandatory	|					      |	string	|						        |
		url			  |	optional	|	current url		|	string	|						        |
		async		  |	optional	|	true			    |	boolean	|	asynchronous call	|
		newItem		|	optional	|	none			    |	object	|	new items values	|	Field names must start with capital letter even if in the list it doesn't
		
==EXAMPLE==
  zNewItem({
    listName: "testList",
    newItem:{
      Role: 'manager',							//field name: value
      Grade: '1', 							//field name: value
      ProjectId: '4', 							//field name: value
      Name: 'Mietek'							//field name: value
    }
  });
 
3.	zModifyItem(parameter) - create new list item in the list and with field values indicated in parameter
	parameter [object]
  
		NAME		  |	MAN./OPT.	|	DEFAULT			    |	TYPE	|	INFO				        |	REMARKS
		listName	|	mandatory	|					      |	string	|						          |
		url			  |	optional	|	current url		|	string	|						          |
		async		  |	optional	|	true			    |	boolean	|	asynchronous call	  |
		id			  |	mandatory	|	none			    |	long	  |	item ID				      |
		newItem		|	optional	|	none			    |	object	|	field and new value	|	Field names must start with capital letter even if in the list it doesn't
	
==EXAMPLE==
  zModifyItem({
    listName:"testList",
    id: 3646,
    itemData:{
      Project: "test project",						//field name: value
      Name: "Mieczyslaw"							//field name: value			
    }
  });
 
4.	zDeleteItem(parameter) - create new list item in the list and with field values indicated in parameter
	parameter [object]

		NAME		  |	MAN./OPT.	|	DEFAULT		   |	TYPE	|	INFO				      |	REMARKS
		listName	|	mandatory	|				      |	string	|						        |
		url			  |	optional	|	current url	|	string	|						        |
		async		  |	optional	|	true		    |	boolean	|	asynchronous call	|
		id			  |	mandatory	|	none		    |	array	  |	item ID(s)			  |	can delete multiple items by ID
	
==EXAMPLE==
  zDeleteItem({
    listName:"testList",
    id: [123,331,121]	
  });
	
