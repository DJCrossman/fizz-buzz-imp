// configure the imp (best practice)
imp.configure("Fizz Buzz Machine", [], []);
 
// Configure pin9
hardware.pin9.configure(DIGITAL_OUT);

local amplitude = 0.15
 
function getFrequency(sound) {
    local freq = 0;
    if (note == "Buzz") freq = 27.50;
    else if (note == " ") freq = 29.1352;
    else if (note == "FizzBuzz") freq = 18.354;
    else if (note == "Fizz") freq = 20.602;
    return freq;
}

function FizzBuzz(msg) {
    server.log("The number is" + msg);
    amplitude = amplitude + 0.05;
    // Fizz Buzz typically only goes to 100 (limited due to time)
    if( msg > 100 ) {
        msg = 100;
    }
    for (local i = 0; i < msg; i++) {
        
        local sound = "";
        
        if(!(i % 3 == 0) && !(i % 5 == 0)) sound = " ";
        if(i % 3 == 0) sound += "Fizz";
        if(i % 5 == 0) sound += "Buzz";
        
        local time = 1.0;
        local frequency = getFrequency(sound);
        hardware.pin1.configure(PWM_OUT, 1.0/frequency, 1.0);
        hardware.pin1.write(amplitude);
        if (amplitude > 0.15) amplitude = amplitude - 0.001;
    }
    hardware.pin1.write(0);
}

agent.on("incoming", FizzBuzz);
