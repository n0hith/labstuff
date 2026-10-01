import 'package:flutter/material.dart';
void main() {
 runApp(const MaterialApp(
   debugShowCheckedModeBanner: false,
   home: RegistrationForm(),
 ));
}
class RegistrationForm extends StatefulWidget {
 const RegistrationForm({super.key});


 @override
 State<RegistrationForm> createState() => _RegistrationFormState();
}
class _RegistrationFormState extends State<RegistrationForm> {
 final formKey = GlobalKey<FormState>();
 String gender = "Male";
 String course = "CSE";


 @override
 Widget build(BuildContext context) {
   return Scaffold(
     appBar: AppBar(
       title: const Text("Registration Form"),
     ),
     body: Padding(
       padding: const EdgeInsets.all(20),
       child: Form(
         key: formKey,


         child: ListView(
           children: [
             // Name
             TextFormField(
               decoration: const InputDecoration(
                 labelText: "Name",


                 border: OutlineInputBorder(),
               ),
               validator: (String? value) {
                 if (value == null || value.isEmpty) {
                   return "Please enter your name";
                 }
                 return null;
               },
             ),
             const SizedBox(height: 15),
             // Email
             TextFormField(
               keyboardType: TextInputType.emailAddress,
               decoration: const InputDecoration(
                 labelText: "Email",
                 border: OutlineInputBorder(),
               ),
               validator: (String? value) {
                 if (value == null || value.isEmpty) {
                   return "Please enter your email";
                 }
                 return null;
               },
             ),


             const SizedBox(height: 15),
             // Password
             TextFormField(
               obscureText: true,
               decoration: const InputDecoration(
                 labelText: "Password",
                 border: OutlineInputBorder(),
               ),
             ),
             const SizedBox(height: 15),
             // Gender


             const Text(
               "Gender",
               style: TextStyle(
                 fontSize: 16,
                 fontWeight: FontWeight.bold,
               ),
             ),
             RadioGroup<String>(
               groupValue: gender,
               onChanged: (String? value) {
                 setState(() {
                   gender = value!;
                 });
               },
               child: Column(
                 children: [
                   RadioListTile<String>(
                     title: const Text("Male"),
                     value: "Male",
                   ),
                   RadioListTile<String>(
                     title: const Text("Female"),
                     value: "Female",
                   ),
                 ],
               ),
             ),
             const SizedBox(height: 10),
             // Course
             DropdownButtonFormField<String>(
               initialValue: course,
               decoration: const InputDecoration(
                 labelText: "Course",
                 border: OutlineInputBorder(),
               ),
               items: const [


                 DropdownMenuItem(
                   value: "CSE",
                   child: Text("CSE"),
                 ),
                 DropdownMenuItem(
                   value: "ECE",
                   child: Text("ECE"),
                 ),
                 DropdownMenuItem(
                   value: "EEE",
                   child: Text("EEE"),
                 ),
                 DropdownMenuItem(
                   value: "MECH",
                   child: Text("MECH"),
                 ),
               ],
               onChanged: (String? value) {
                 setState(() {
                   course = value!;
                 });
               },
             ),
             const SizedBox(height: 20),
             // Submit
             ElevatedButton(
               onPressed: () {
                 if (formKey.currentState!.validate()) {
                   ScaffoldMessenger.of(context).showSnackBar(
                     const SnackBar(
                       content: Text("Form Submitted Successfully"),
                     ),
                   );
                 }
               },
               child: const Text("Submit"),


             ),
           ],
         ),
       ),
     ),
   );
 }
}