# homework_18_09_23
Андреев Владимир 
Хабибулина Кристина 
ИП-11
  using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Text.RegularExpressions;
namespace StringCheckLib
{
    public class StringCheck
    {
        /// <summary>
        /// Проверка stringName на наличие симоволов: Русские буквы, пробел и дефис.
        /// Строка stringName не должна привишать 50 символов.
        /// </summary>
        /// <param name="stringname"></param>
        /// <returns>
        /// true or false
        /// </returns>
        public static bool CheckName(string stringname)
        {
            string jopa = @"^(([а-я])|(\s)|(\-))+$";
            string jopaWhiteSpace = @"^((\s)|(\-))+$";
            if (stringname.Length > 50)
            {
                return false;
            }
            if (Regex.Match(stringname, jopaWhiteSpace, RegexOptions.IgnoreCase).Success)
            {
                return false;
            }
            else
            {
                if (Regex.Match(stringname, jopa, RegexOptions.IgnoreCase).Success)
                {
                    return true;
                }
                else
                {
                    return false;
                }
            }
        }
    }
}


-------------------------------------------------------------------------------


using Microsoft.VisualStudio.TestTools.UnitTesting;
using System;
using StringCheckLib;

namespace StringCheckLibTest
{
    /// <summary>
    /// Проверка на правильность написания ФИО
    /// </summary>
    [TestClass]
    public class UnitTest1
    {
        [TestMethod]
        public void CheckName_Space_FalseReturned()
        {
            //Arrange
            string stringname = " ";
            //Act
            bool result = StringCheck.CheckName(stringname);
            //Assert
            Assert.IsFalse(result);
        }
        [TestMethod]
        public void CheckName_Dash_FalseReturned()
        {
            //Arrange
            string stringname = "-";
            //Act
            bool result = StringCheck.CheckName(stringname);
            //Assert
            Assert.IsFalse(result);
        }
        [TestMethod]
        public void CheckName_UseSymbol_FalseReturned()
        {
            //Arrange
            string stringname = "Андреев Владимир Павлович/";
            //Act
            bool result = StringCheck.CheckName(stringname);
            //Assert
            Assert.IsFalse(result);
        }
        [TestMethod]
        public void CheckName_IsTooLong_FalseReturned()
        {
            //Arrange
            string stringname = "АндреевАндреевАндреевАндреевАндреевАндреевАндреевАндреевАндреевАндреев Владимир Павлович";
            //Act
            bool result = StringCheck.CheckName(stringname);
            //Assert
            Assert.IsFalse(result);
        }
        [TestMethod]
        public void CheckName_UseDigits_FalseReturned()
        {
            //Arrange
            string stringname = "Андреев1 Владимир Павлович";
            //Act
            bool result = StringCheck.CheckName(stringname);
            //Assert
            Assert.IsFalse(result);
        }
        [TestMethod]
        public void CheckName_CorrectWriting_TrueReturned()
        {
            //Arrange
            string stringname = "Андреев Владимир Павлович";
            //Act
            bool result = StringCheck.CheckName(stringname);
            //Assert
            Assert.IsTrue(result);
        }
    }
}
