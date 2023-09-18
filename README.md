# Using_Regular_Expressions
-Lib

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
                    string regex = @"^(([а-я])|(\s)|(\-))+$";
                    string regexWhiteSpace = @"^((\s)|(\-))+$";
                    if(stringname.Length>50)
                    {
                        return false;
                    }
                    if(Regex.Match(stringname, regexWhiteSpace,RegexOptions.IgnoreCase).Success )
                    {
                        return false;
                    }
                    else
                    {
                        if (Regex.Match(stringname, regex, RegexOptions.IgnoreCase).Success)
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
        
-Test

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
            public void CheckName_IsEmpty_FalseReturned()
            {
                //Arrange
                string stringname = " ";
                //Act
                bool result = StringCheck.CheckName(stringname);
                //Assert
                Assert.IsFalse(result);
            }
            [TestMethod]
            public void CheckName_IsDash_FalseReturned()
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
                string stringname = "Казанцев Денис Сергеевич/";
                //Act
                bool result = StringCheck.CheckName(stringname);
                //Assert
                Assert.IsFalse(result);
            }
            [TestMethod]
            public void CheckName_IsTooLong_FalseReturned()
            {
                //Arrange
                string stringname = "КазанцевКазанцевКазанцевКазанцевКазанцев Денис Сергеевич";
                //Act
                bool result = StringCheck.CheckName(stringname);
                //Assert
                Assert.IsFalse(result);
            }
            [TestMethod]
            public void CheckName_UseDigits_FalseReturned()
            {
                //Arrange
                string stringname = "Казанцев1 Денис Сергеевич";
                //Act
                bool result = StringCheck.CheckName(stringname);
                //Assert
                Assert.IsFalse(result);
            }
            [TestMethod]
            public void CheckName_CorrectWriting_TrueReturned()
            {
                //Arrange
                string stringname = "Казанцев Денис Сергеевич";
                //Act
                bool result = StringCheck.CheckName(stringname);
                //Assert
                Assert.IsTrue(result);
            }
        }
    }
    
    
    
            
