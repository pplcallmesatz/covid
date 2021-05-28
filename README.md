### Get the TamilNadu COVID Beds details from the [Tamil Nadu COVID Beds](https://tncovidbeds.tnega.org/)


---


**Step 1:** Go to the [https://tncovidbeds.tnega.org/](https://tncovidbeds.tnega.org/)

**Step 2:** Choose the `District` from dropdown

**Step 3:** Open the `browser inspect window` 

**Step 4:** Run the below code in the `console tab`. Make sure you have updated the API before running the below code in console.

Below code is created for APISPreadSheet.

````
var i = 1;   
var toLen = $('#bedTable #tableBody tr').length;
function myLoop() {         
  setTimeout(function() {   
    var thiss = $('#bedTable #tableBody tr:nth-child('+i+')');   				//Get the table row
    var hospital = $(thiss).find("td:nth-child(1) > *:nth-child(1)").text();			//Get the Hospital name
    var hospitalMap = $(thiss).find("td:nth-child(1) > *:nth-child(1) a").attr("href");		//Get the Hospital Map
    var Address = $(thiss).find("td:nth-child(1) > *:nth-child(3)").text();			//Get the Hospital Address
    var phone = $(thiss).find("td:nth-child(1) > *:nth-child(7)").text();			//Get the Hospital phone number
    var lastUpdated = $(thiss).find("td:nth-child(1) > *:nth-child(9)").text();			//Get the Hospital last updated date
    var totalNormalBed = $(thiss).find("td:nth-child(2)").text();				//Get the Total Normal Bed
    var totalNormalBedVacant = $(thiss).find("td:nth-child(3)").text();				//Get the Total Normal Vacant Bed
    var totalOxygenBed = $(thiss).find("td:nth-child(4)").text();				//Get the Total Oxygen Bed
    var totalOxygenBedVacant = $(thiss).find("td:nth-child(5)").text();				//Get the Total Oxygen Vacant Bed
    var totalICUBed = $(thiss).find("td:nth-child(6)").text();					//Get the Total ICU Bed
    var totalICUBedVacant = $(thiss).find("td:nth-child(7)").text();				//Get the Total ICU Vacant Bed
    var totalBed = $(thiss).find("td:nth-child(8)").text();					//Get the Total Bed
    var totalBedVacant = $(thiss).find("td:nth-child(9)").text();				//Get the Total Vacant Bet
    var formHtml ='<form id="myData"><label>hospital</label><input value="'+hospital+'" name="hospital" /><br/><label>hospitalMap</label><input name="hospitalMap"                      value="'+hospitalMap+'" /><br/><label>Address</label><input name="Address" value="'+Address+'" /><br/><label>phone</label><input name="phone"                         value="'+phone+'"/><br/><label>lastUpdated</label><input name="lastUpdated" value="'+lastUpdated+'"/><br/><label>totalNormalBed</label><input                     name="totalNormalBed" value="'+totalNormalBed+'" /><br/><label>totalNormalBedVacant</label><input name="totalNormalBedVacant"                                       value="'+totalNormalBedVacant+'" /><br/><label>totalOxygenBed</label><input name="totalOxygenBed" value="'+totalOxygenBed+'"/><br/>                                 <label>totalOxygenBedVacant</label><input name="totalOxygenBedVacant" value="'+totalOxygenBedVacant+'"/><br/><label>totalICUBed</label><input                       name="totalICUBed" value="'+totalICUBed+'"/><br/><label>totalICUBedVacant</label><input name="totalICUBedVacant" value="'+totalICUBedVacant+'" />                   <br/><label>totalBed</label><input value="'+totalBed+'" name="totalBed" /><br/><label>totalBedVacant</label><input name="totalBedVacant"                              value="'+totalBedVacant+'" />	</form>';
     $("body").append(formHtml);
    var  da = $("#myData").serializeArray()

    SubForm(da, $(thiss));  // Submit the form data
    $('#myData').remove();
    
    
     //  your code here
     i++;                    
     if (i <= toLen) {       
        myLoop();             
      }                       
    }, 3000)			// Delay function in order to prevent the continious hit
  }

myLoop();     
function SubForm(data, th){
			$.ajax({
				url:"{ Your API Spread Sheet API Code}",	//You can use the APISpreadSheet/Google firebase
				type:"post",
				data:data,
				success: function(){
                			console.log(data[0].value);  //Print the Name of the Hospital
                			th.css("opacity", "0.1");   //Apply opacity to the table in order to validate that row is fetched
				},
				error: function(){
					alert("There was an error :(")
				}
			});
		}


````
