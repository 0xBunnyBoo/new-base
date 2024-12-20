// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract ControlStructures {
    // Custom error definitions for contract
    error AfterHours(uint256 time);
    error AtLunch();

    // FizzBuzz function to check the input number and return result
    function fizzBuzz(uint256 _number) public pure returns (string memory response) {
        if (_number % 3 == 0 && _number % 5 == 0) {
            return "FizzBuzz"; // Return "FizzBuzz" if the number is divisible by 3 and 5
        }
        if (_number % 3 == 0) {
            return "Fizz"; // Return "Fizz" if the number is divisible by 3
        }
        if (_number % 5 == 0) {
            return "Buzz"; // Return "Buzz" if the number is divisible by 5
        }
        return "Splat"; // Return "Splat" if none of the conditions are met
    }

    // doNotDisturb function to check input time and return result
    function doNotDisturb(uint256 _time) public pure returns (string memory result) {
        // Check if time is valid (less than 2400)
        require(_time < 2400, "Invalid time input"); // Time should be less than 2400
        require(_time % 100 < 60, "Invalid minute format"); // Minutes should be less than 60

        // Check different time ranges and return appropriate response or throw errors
        if (_time > 2200 || _time < 800) {
            revert AfterHours(_time); // Custom error if time is greater than 2200 or less than 800
        }
        if (_time >= 1200 && _time <= 1299) {
            revert AtLunch(); // Custom error if time is between 1200 and 1299 (lunch time)
        }
        if (_time >= 800 && _time <= 1199) {
            return "Morning!"; // Return "Morning!" if time is between 800 and 1199
        }
        if (_time >= 1300 && _time <= 1799) {
            return "Afternoon!"; // Return "Afternoon!" if time is between 1300 and 1799
        }
        if (_time >= 1800 && _time <= 2200) {
            return "Evening!"; // Return "Evening!" if time is between 1800 and 2200
        }
    }
}
