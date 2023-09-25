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
    using System.Security.AccessControl;

    namespace PasswordCheckLibTEST
    {

    [TestClass]
    public class PasswordCheckerTests
    {
        /// <summary>
        /// Корректный пароль
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
        /// Пустое поле ввода
        /// </summary>
        [TestMethod]
        public void Check_Password_NullorEmoty_False()
        {
            // Arrange
            string password = " ";
            bool expected = false;
            // Act
            bool actual = PasswordChecker.ValidatePassword(password);
            // Asserts
            Assert.AreEqual(expected, actual);
        }
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
        [TestMethod]
        public void Sozdayom_prikol ()
        {
            string password = "";
            string lett = "abcdefghijklmnopqrstuvwxyz";
            string letter = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
            string digits = "1234567890";
            string spec = "#$%^&_";
            Random rnd = new Random();
            int konec = rnd.Next(8, 20);
            while (password.Length <= konec)
            {


                int zxc = rnd.Next(0, 4);
                if (zxc == 0)
                {
                    int z = rnd.Next(lett.Length);
                    char z1 = (char)('a' + z);
                    password = password + z1;

                }
                if (zxc == 1)
                {
                    int z = rnd.Next(letter.Length);
                    char x1 = (char)('A' + z);
                    password = password + x1;

                }
                if (zxc == 2)
                {
                    int z = rnd.Next(letter.Length);
                    char c1 = (char)('1' + z);
                    password = password + c1;

                }
                if (zxc == 3)
                {
                    int z = rnd.Next(letter.Length);
                    char v1 = (char)('!' + z);
                    password = password + v1;

                }

            }
            bool exepted = true;
            bool actual = PasswordChecker.ValidatePassword(password);
            Assert.IsTrue(actual);
        }
    }
}

