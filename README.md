# Commit-2-Source-Code-Improvements

//I, Harshitkumar Jadhav, 000771381 certify that this material is my original work. No other person's work has been used without due acknowledgement.

using System;
using System.Collections.Generic;


/// <summary>
/// This is main class called A4 and project name is COMP10066_Lab4 which contains all method to display output. 
/// </summary>
namespace COMP10066_Lab4
{
    /**
     * Library of statistical functions using Generics for different statistical
     * calculations.
     * 
     * see http://www.calculator.net/standard-deviation-calculator.html
     * for sample standard deviation calculations
     *
     * @author Joey Programmer
     */

    public class A4
    {
        /// <summary>
        /// This is a Average method which will calculate the average of real number.
        /// </summary>
        /// <param name="numbers"> This is a list of precision number with datatype double.</param>
        /// <param name="negativeNumbers"> This is a boolean value which will result TRUE or FALSE, that 
        /// negative number are excluded in calculating the average or not. </param>
        /// <returns>Precision value with datatype double which is the total of numbers.</returns>
        public static double Average(List<double> numbers, bool negativeNumbers)
        {
            // Calculating the total set of samples
            double sumOfValue = Sum(numbers, negativeNumbers);
            int valueCount = 0;

            // For loop which will make if condition and return the average of total value divided by value count
            for (int i = 0; i < numbers.Count; i++)
            {
                // if condition for increment  
                if (negativeNumbers || numbers[i] >= 0)
                {
                    valueCount++;
                }
            }

            // if condition that will throw exception 
            if (valueCount == 0)
            {
                throw new ArgumentException("no values are > 0");
            }
            return sumOfValue / valueCount;
        }

        /// <summary>
        /// This is a Sum method which will calculate the sum of real number.
        /// </summary>
        /// <param name="numbers">This is a list of precision number with datatype double.</param>
        /// <param name="negativeNumbers"> This is a boolean value which will result TRUE or FALSE, that 
        /// negative number are excluded in calculating the average or not. </param>
        /// <returns>Precision value with datatype double which is the total of numbers.</returns>
        public static double Sum(List<double> numbers, bool negativeNumbers)
        {
            //if condition for x not be an empty with exception message 
            if (numbers.Count < 0)
            {
                throw new ArgumentException("x cannot be empty");
            }

            // calculate the total value
            double sum = 0.0;
            foreach (double val in numbers)
            {
                // Include negativeNumbers 
                if (negativeNumbers || val >= 0)
                {
                    sum += val;
                }
            }
            return sum;
        }

        /// <summary>
        /// This is a Median method which will calculate the median of real number.
        /// </summary>
        /// <param name="data">This is a list of precision number with datatype double.</param>
        /// <returns>Precision value with datatype double which is the median of numbers.</returns>
        public static double Median(List<double> data)
        {
            // if condition for data count to be empty and will throw exception 
            if (data.Count == 0)
            {
                throw new ArgumentException("Size of array must be greater than 0");
            }

            // Sorting data in ascending order by default.
            data.Sort();

            // calculating the median with the data count divided by 2
            double median = data[data.Count / 2];
            if (data.Count % 2 == 0)
                median = (data[data.Count / 2] + data[data.Count / 2 - 1]) / 2;
            // return median value
            return median;
        }

        /// <summary>
        /// This is a standard deviation method which will calculate the standard deviation of real number.
        /// </summary>
        /// <param name="data">This is a list of precision number with datatype double.</param>
        /// <returns>Precision value with datatype double which is the standard deviation of numbers.</returns>
        public static double standardDeviation(List<double> data)
        {
            // if condition for data count to be less than or equal to 1, 
            // which will throw exception message 
            if (data.Count <= 1)
            {
                throw new ArgumentException("Size of array must be greater than 1");
            }

            // Initializing variables
            int numberCount = data.Count;
            double standard = 0;
            double average = Average(data, true);

            // for loop which will return standardDeviation
            for (int i = 0; i < numberCount; i++)
            {
                double v = data[i];
                standard += Math.Pow(v - average, 2);
            }

            // calculate standard deviation as a square root of standard 
            double standardDeviation = Math.Sqrt(standard / (numberCount - 1));

            //return standard deviation
            return standardDeviation;
        }

        // Simple set of tests that confirm that functions operate correctly
        static void Main(string[] args)
        {
            List<Double> testDataD = new List<Double> { 2.2, 3.3, 66.2, 17.5, 30.2, 31.1 };

            // Display output 
            Console.WriteLine("The sum of the array = {0}", Sum(testDataD, true));

            Console.WriteLine("The average of the array = {0}", Average(testDataD, true));

            Console.WriteLine("The median value of the Double data set = {0}", Median(testDataD));

            Console.WriteLine("The sample standard deviation of the Double test set = {0}\n", standardDeviation(testDataD));
        }
    }
}
