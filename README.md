# Password_complexity_testing
Create By: Денис Казанцев & Артем Николаев
-Lib

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    
    namespace PasswordCheckLib
    {
        public class PasswordChecker
        {
            /// <summary>
            /// Проверка пароля на соответствие заданным параметрам
            /// </summary>
            /// <param name="password"></param>
            /// <returns>
            /// Проверяет пароль на соответствие 
            /// </returns>
            public static bool ValidatePassword (string password)
            {
                if (password.Length < 8 || password.Length > 20)
                {
                    return false; 
                }
                if(!password.Any(Char.IsLower))
                {
                    return false;
                }
                if (!password.Any(Char.IsUpper))
                {
                    return false;
                }
                if (!password.Any(Char.IsDigit))
                {
                    return false;
                }
                if(password.Intersect("#$%^&_").Count()== 0)
                {
                   return false;
                }
                return true;
    
            }
        }
    }
    
-Tests


    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System;
    using PasswordCheckLib;
    
    namespace PasswordCheckLibTEST
    {
        [TestClass]
        public class UnitTest1
        { 
            /// <summary>
            /// Без строчных букв
            /// </summary>
            [TestMethod]
            public void Check_PasswordWithoutLowerSymbols_False()
            {
                // Arrange
                string password = "ASDQWE123$";
                bool expected = false;
                // Act
                bool actual = PasswordChecker.ValidatePassword(password);
                // Asserts
                Assert.AreEqual(expected,actual);
            }
            /// <summary>
            /// Пароль С верхним и нижним регистром
            /// </summary>
            [TestMethod]
            public void Check_PasswordWithUpperandLowerSymbols_True()
            {
                // Arrange
                string password = "ASDqwe1$";
                bool expected = true;
                // Act
                bool actual = PasswordChecker.ValidatePassword(password);
                // Asserts
                Assert.AreEqual(expected, actual);
            }
            /// <summary>
            /// Пароль менее 8 символов
            /// </summary>
            [TestMethod]
            public void Check_PasswordLengthlessthen8symbols_false()
            {
                // Arrange
                string password = "Aq1$";
                bool expected = false;
                // Act
                bool actual = PasswordChecker.ValidatePassword(password);
                // Asserts
                Assert.AreEqual(expected, actual);
            }
            /// <summary>
            /// Пароль равен 8 символам
            /// </summary>
            [TestMethod]
            public void Check_PasswordLengthEqual8symbols_True()
            {
                // Arrange
                string password = "ASqw12$$";
                bool expected = true;
                // Act
                bool actual = PasswordChecker.ValidatePassword(password);
                // Asserts
                Assert.AreEqual(expected, actual);
            }
            /// <summary>
            /// Пароль больше чем 20 символов
            /// </summary>
            [TestMethod]
            public void Check_PasswordLengthMoreThen20Symbols_False()
            {
                // Arrange
                string password = "ASDqwe123$ASDqwe123$ASDqwe123$";
                bool expected = false;
                // Act
                bool actual = PasswordChecker.ValidatePassword(password);
                // Asserts
                Assert.AreEqual(expected, actual);
            }
            /// <summary>
            /// В пароле есть цифры
            /// </summary>
            [TestMethod]
            public void Check_PasswordHasDigits_True()
            {
                // Arrange
                string password = "ASDqwe1$";
                bool expected = true;
                // Act
                bool actual = PasswordChecker.ValidatePassword(password);
                // Asserts
                Assert.AreEqual(expected, actual);
            }
            /// <summary>
            /// Пароль не имеет цифры
            /// </summary>
            [TestMethod]
            public void Check_PasswordHasDigits_False()
            {
                // Arrange
                string password = "ASDqweASD$";
                bool expected = false;
                // Act
                bool actual = PasswordChecker.ValidatePassword(password);
                // Asserts
                Assert.AreEqual(expected, actual);
            }
            /// <summary>
            /// В пароле присутствуют спец символы
            /// </summary>
            [TestMethod]
            public void Check_PasswordHasSpecSymbols_True()
            {
                // Arrange
                string password = "Aqwe123$";
                bool expected = true;
                // Act
                bool actual = PasswordChecker.ValidatePassword(password);
                // Asserts
                Assert.AreEqual(expected, actual);
            }
            /// <summary>
            /// В пароле отсутствуют спец символов
            /// </summary>
            [TestMethod]
            public void Check_PasswordHasSpecSymbols_False ()
            {
                // Arrange
                string password = "ASDqwe123";
                bool expected = false;
                // Act
                bool actual = PasswordChecker.ValidatePassword(password);
                // Asserts
                Assert.AreEqual(expected, actual);
            }
            /// <summary>
            /// В пароле есть прописные буквы
            /// </summary>
            [TestMethod]
            public void Check_PasswordHasUpperSymbols_True()
            {
                // Arrange
                string password = "Aqwe123$";
                bool expected = true;
                // Act
                bool actual = PasswordChecker.ValidatePassword(password);
                // Asserts
                Assert.AreEqual(expected, actual);
            }
            /// <summary>
            /// В паролы отсутствуют прописные буквы
            /// </summary>
            [TestMethod]
            public void Check_PasswordHasUpperSymbols_False()
            {
                // Arrange
                string password = "asdqwe123$";
                bool expected = false;
                // Act
                bool actual = PasswordChecker.ValidatePassword(password);
                // Asserts
                Assert.AreEqual(expected, actual);
            }
            /// <summary>
            /// В пароле встречаются строчные буквы
            /// </summary>
            [TestMethod]
            public void Check_PasswordHasLowerSymbols_True()
            {
                // Arrange
                string password = "ASDq123$";
                bool expected = true;
                // Act
                bool actual = PasswordChecker.ValidatePassword(password);
                // Asserts
                Assert.AreEqual(expected, actual);
            }
            /// <summary>
            /// В пароле отсутствуют строчные буквы
            /// </summary>
            [TestMethod]
            public void Check_PasswordHasLowerSymbols_False ()
            {
                // Arrange
                string password = "ASDQWE123$";
                bool expected = false;
                // Act
                bool actual = PasswordChecker.ValidatePassword(password);
                // Asserts
                Assert.AreEqual(expected, actual);
            }
        }
        }
