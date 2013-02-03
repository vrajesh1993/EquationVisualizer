$(document).ready(function(){
var container = document.getElementById('container');
var start = (new Date).getTime();
var data, graph, offset, i;

var mode = 1;
var fmode1 = 1; // 1- basic sin, 2 - sin(1/x)
var fmode2 = 2;
var operator = 0;
var offset1 = 0;
var offset2 = 0;
//data = [];
//data2 =[];
function getValue(i,j)
{
	//alert(i);
	if(i==1) return Math.sin(j);
	if(i==2) return Math.cos(j);
	if(i==3) return Math.tan(j);
	if(i==4) return Math.asin(j);
}

function genValue(op, val1, val2){
	if (op == 1) return val1 + val2;
	if (op == 2) return val1 - val2;
	if (op == 3) {
		return val1 / val2;
	}
	if (op == 4) return val1 * val2;
}

// Draw a sine curve at time t
function animateSine (t) {
    data1 = [];
    data2 = [];
	data3 = [];

    // little offset between steps
    offset = 2 * Math.PI * (t - start) / 10000;

    if (offset > 15) {
        start = t;
    }
	 offset1=offset2=0;
    for (i = 0; i < 4 * Math.PI; i += 0.2) {
		var val1 = getValue(fmode1,(i - offset+(offset1/(2*Math.PI))));
		var val2 = getValue(fmode2,(i - offset+(offset2/(2*Math.PI))));
         data1.push([val1, -i + 10]);
		 data2.push([val2, -i + 10]);
		 data3.push([genValue(operator, val1, val2), -i + 10]);
    }
    // prepare properties
    var properties;
    switch (mode) {
        case 1:
            properties = {
                yaxis : {
                    max : 10,
                    min : 0
                },
				xaxis : {
                    max : 2,
                    min : -2
                },
            };
            break;
        case 2:
            properties = {
                yaxis : {
                    max : 2,
                    min : -2
                },
                bars: {
                    show: true,
                    horizontal: false,
                    shadowSize: 0,
                    barWidth: 0.5
                }
            };
            break;
        case 3:
            properties = {
                yaxis : {
                    max : 2,
                    min : -2
                },
                radar: {
                    show: true
                },
                grid: {
                    circular: true,
                    minorHorizontalLines: true
                }
            };
            break;
        case 4:
            properties = {
                yaxis : {
                    max : 2,
                    min : -2
                },
                bubbles: {
                    show: true,
                    baseRadius: 5
                },
            };
            break;
    }

    // draw graph
	if(operator == 0 || fmode2 == 0){
		if (fmode1 > 0 && fmode2>0) {
			graph = Flotr.draw(container, [ data1, data2], properties);
		} else if (fmode1 < 1 && fmode2>0) {
			graph = Flotr.draw(container, [ data2], properties);
		}else if (fmode1 > 0 & fmode2<1) {
			graph = Flotr.draw(container, [ data1], properties);
		}
	}
	else{
		graph = Flotr.draw(container, [ data3], properties);
	}
	

    // main loop
    setTimeout(function () {
        animateSine((new Date).getTime());
    }, 50);
}

$('#function1').change(function(){
	//alert($('#function1').val());
	fmode1 = $('#function1').val();
});

$('#function2').change(function(){
	//alert($('#function2').val());
	fmode2 = $('#function2').val();
});

$('#operator').change(function(){
	operator = $('#operator').val();
});

$('#offset2').keyup(function(){
	offset2 = Number($('#offset2').val())//Math.PI;
	//offset2=0;
	 //alert(Number(offset2));
});
$('#offset1').keyup(function(){
	offset1 = Number($('#offset1').val())//(4*Math.PI);
	//offset1=0;
	 //alert(Number(offset1));
});

animateSine(start);

});
