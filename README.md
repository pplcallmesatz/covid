# Get the TamilNadu COVID Beds details from the [Tamil Nadu COVID Beds](https://tncovidbeds.tnega.org/)


**Step 1: ** Go to the [https://tncovidbeds.tnega.org/](https://tncovidbeds.tnega.org/)

**Step 2: ** Choose the >District from dropdown

**Step 3: ** Open the browser inspect tab

**Step 4: ** Run the below code in the console tab

````
var i = 1;   
var toLen = $('#bedTable #tableBody tr').length;
function myLoop() {         
  setTimeout(function() {   
    var thiss = $('#bedTable #tableBody tr:nth-child('+i+')');
    var hospital = $(thiss).find("td:nth-child(1) > *:nth-child(1)").text();
    var hospitalMap = $(thiss).find("td:nth-child(1) > *:nth-child(1) a").attr("href");
    var Address = $(thiss).find("td:nth-child(1) > *:nth-child(3)").text();
    var phone = $(thiss).find("td:nth-child(1) > *:nth-child(7)").text();
    var lastUpdated = $(thiss).find("td:nth-child(1) > *:nth-child(9)").text();
    var totalNormalBed = $(thiss).find("td:nth-child(2)").text();
    var totalNormalBedVacant = $(thiss).find("td:nth-child(3)").text();
    var totalOxygenBed = $(thiss).find("td:nth-child(4)").text();
    var totalOxygenBedVacant = $(thiss).find("td:nth-child(5)").text();
    var totalICUBed = $(thiss).find("td:nth-child(6)").text();
    var totalICUBedVacant = $(thiss).find("td:nth-child(7)").text();
    var totalBed = $(thiss).find("td:nth-child(8)").text();
    var totalBedVacant = $(thiss).find("td:nth-child(9)").text();
    var formHtml ='<form id="myData"><label>hospital</label><input value="'+hospital+'" name="hospital" /><br/><label>hospitalMap</label><input name="hospitalMap"                      value="'+hospitalMap+'" /><br/><label>Address</label><input name="Address" value="'+Address+'" /><br/><label>phone</label><input name="phone"                         value="'+phone+'"/><br/><label>lastUpdated</label><input name="lastUpdated" value="'+lastUpdated+'"/><br/><label>totalNormalBed</label><input                     name="totalNormalBed" value="'+totalNormalBed+'" /><br/><label>totalNormalBedVacant</label><input name="totalNormalBedVacant"                                       value="'+totalNormalBedVacant+'" /><br/><label>totalOxygenBed</label><input name="totalOxygenBed" value="'+totalOxygenBed+'"/><br/>                                 <label>totalOxygenBedVacant</label><input name="totalOxygenBedVacant" value="'+totalOxygenBedVacant+'"/><br/><label>totalICUBed</label><input                       name="totalICUBed" value="'+totalICUBed+'"/><br/><label>totalICUBedVacant</label><input name="totalICUBedVacant" value="'+totalICUBedVacant+'" />                   <br/><label>totalBed</label><input value="'+totalBed+'" name="totalBed" /><br/><label>totalBedVacant</label><input name="totalBedVacant"                              value="'+totalBedVacant+'" />	</form>';
     $("body").append(formHtml);
    var  da = $("#myData").serializeArray()

    SubForm(da, $(thiss));
    $('#myData').remove();
    
    
     //  your code here
     i++;                    
     if (i <= toLen) {       
        myLoop();             
      }                       
    }, 3000)
  }

myLoop();     
function SubForm(data, th){
			$.ajax({
				url:"{ Your API Spread Sheet API Code}",
				type:"post",
				data:data,
				success: function(){
                console.log(data[0].value);
                th.css("opacity", "0.1");
				},
				error: function(){
					alert("There was an error :(")
				}
			});
		}


````
