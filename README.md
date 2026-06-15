# java-script
// 10+ foydalanuvchi ma'lumotlaridan iborat baza (Array)
const users = [
  { id: 1, name: "Ali", age: 24, email: "ali@example.com", address: { city: "Toshkent", street: "Amir Temur" } },
  { id: 2, name: "Zuhra", age: 19, email: "zuhra@example.com", address: { city: "Samarqand", street: "Registon" } },
  { id: 3, name: "Olim", age: 30, email: "olim@example.com", role: "admin", address: { city: "Buxoro", street: "Navoiy" } },
  { id: 4, name: "Malika", age: 22, email: "malika@example.com", address: { city: "Andijon", street: "Bobur" } },
  { id: 5, name: "Sardor", age: 28, email: "sardor@example.com", address: { city: "Farg'ona", street: "Sayilgohi" } },
  { id: 6, name: "Madina", age: 25, email: "madina@example.com", role: "moderator", address: { city: "Namangan", street: "Istiqlol" } },
  { id: 7, name: "Jasur", age: 35, email: "jasur@example.com", address: { city: "Xiva", street: "Pahlavon Mahmud" } },
  { id: 8, name: "Gulnoza", age: 21, email: "gulnoza@example.com", address: { city: "Nukus", street: "Berdaq" } },
  { id: 9, name: "Farruh", age: 27, email: "farruh@example.com", address: { city: "Navoiy", street: "Tinchlik" } },
  { id: 10, name: "Laylo", age: 23, email: "laylo@example.com", address: { city: "Jizzax", street: "Sharaf Rashidov" } }
];

// 1. Destructuring funksiya parametrida, Default qiymat va Nested destructuring
const transformProfile = ({ name, age, email, role = 'user', address: { city } }) => {
  // Eski string konkatenatsiya o'rniga Template Literals (`...`)
  return {
    displayName: `${name} (${age} yosh)`,
    contact: email,
    accessLevel: role.toUpperCase(),
    location: city
  };
};

// 2. Rest parametr (...args) ishlatilgan funksiya
const logProfiles = (...profiles) => {
  profiles.forEach(profile => console.log(profile));
};
// Baza uchun dastlabki bitta foydalanuvchini tanlab olamiz
const originalUser = users[0]; // Ali

// 1-Misol: Foydalanuvchi rolini yangilash (role qo'shish)
const updatedRoleUser = {
  ...originalUser,
  role: 'superadmin'
};

// 2-Misol: Foydalanuvchi yoshini oshirish va emailini o'zgartirish
const updatedInfoUser = {
  ...originalUser,
  age: originalUser.age + 1,
  email: "ali.new@example.com"
};

// 3-Misol: Obyekt ichidagi nested (ichma-ich) obyektni xavfsiz yangilash (Manzilni o'zgartirish)
const updatedAddressUser = {
  ...originalUser,
  address: {
    ...originalUser.address,
    street: "Yunusobod 19-kvartal"
  }
};
console.log("--- 1. Barcha profillarni transformatsiya qilish ---");
const transformedUsers = users.map(transformProfile);
console.log(transformedUsers);

console.log("\n--- 2. Rest parametr orqali bir nechta profilni konsolga chiqarish ---");
logProfiles(transformedUsers[0], transformedUsers[1], transformedUsers[2]);

console.log("\n--- 3. Immutable Update natijalari ---");
console.log("Asl foydalanuvchi (O'zgarmagan):", originalUser.address.street); // "Amir Temur"
console.log("Yangilangan manzil (Nusxa):", updatedAddressUser.address.street); // "Yunusobod 19-kvartal"
