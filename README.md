import 'package:flutter/material.dart';
import 'package:firebase_auth/firebase_auth.dart';
import 'package:voting_app/widgets/My_app/image_logiin.dart';
import 'package:voting_app/widgets/My_app/log_in.dart';
import 'package:firebase_core/firebase_core.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: signUp(),
    );
  }
}

class signUp extends StatefulWidget {
  const signUp({super.key});

  @override
  State<signUp> createState() => _SignUpState();
}

class _SignUpState extends State<signUp> {
  final emailController = TextEditingController();
  final passwordController = TextEditingController();

  Future<void> signUp() async {
    try {
      await FirebaseAuth.instance.createUserWithEmailAndPassword(
        email: emailController.text.trim(),
        password: passwordController.text.trim(),
      );
      // Navigate to another screen or show a success message
    } on FirebaseAuthException catch (e) {
      // Handle error
      print(e.message);
      showDialog(
        context: context,
        builder: (context) => AlertDialog(
          content: Text(e.message ?? "An unknown error occurred"),
        ),
      );
    }
  }

  FirebaseAuth _auth = FirebaseAuth.instance;

  @override
  Widget build(BuildContext context) {
    return Container(
      decoration: BoxDecoration(
        color: Colors.black87,
        image: DecorationImage(
          image: AssetImage("assets2/light.jpeg"),
          alignment: Alignment.topLeft,
          fit: BoxFit.fill,
          colorFilter: ColorFilter.mode(Colors.redAccent, BlendMode.color),
        ),
      ),
      padding: EdgeInsets.all(30),
      child: Scaffold(
        backgroundColor: Colors.transparent,
        resizeToAvoidBottomInset: true,
        body: SingleChildScrollView(
          child: Column(
            children: [
              Container(
                alignment: Alignment.topLeft,
                child: Text(
                  "Create Account",
                  style: TextStyle(
                    decoration: TextDecoration.none,
                    fontFamily: 'Arial',
                    fontSize: 49,
                    color: Colors.black,
                  ),
                ),
              ),
              SizedBox(height: MediaQuery.of(context).size.height * 0.04),
              Container(
                padding: EdgeInsets.only(right: 15, left: 10),
                child: Column(
                  children: [
                    TextField(
                      cursorColor: Colors.lightBlueAccent,
                      style: TextStyle(color: Colors.black87, fontSize: 17),
                      decoration: InputDecoration(
                        hintText: 'Name',
                        hintStyle: TextStyle(color: Colors.black87, fontSize: 17),
                        focusColor: Colors.green,
                        focusedBorder: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(20),
                          borderSide: BorderSide(
                            color: Colors.pink,
                            width: 4,
                          ),
                        ),
                        enabledBorder: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(20),
                          borderSide: BorderSide(
                            color: Colors.grey,
                            width: 4,
                          ),
                        ),
                        suffixIcon: Icon(Icons.supervised_user_circle, color: Colors.pink),
                      ),
                    ),
                    SizedBox(height: 10),
                    TextField(
                      cursorColor: Colors.lightBlueAccent,
                      style: TextStyle(color: Colors.black87, fontSize: 17),
                      decoration: InputDecoration(
                        hintText: 'Phone_No',
                        hintStyle: TextStyle(color: Colors.black87, fontSize: 17),
                        focusColor: Colors.green,
                        focusedBorder: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(20),
                          borderSide: BorderSide(
                            color: Colors.pink,
                            width: 5,
                          ),
                        ),
                        enabledBorder: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(20),
                          borderSide: BorderSide(
                            color: Colors.grey,
                            width: 4,
                          ),
                        ),
                        suffixIcon: Icon(Icons.phone, color: Colors.pink),
                      ),
                    ),
                    SizedBox(height: 10),
                    TextField(
                      controller: emailController,
                      keyboardType: TextInputType.emailAddress,
                      cursorColor: Colors.lightBlueAccent,
                      style: TextStyle(color: Colors.black87, fontSize: 17),
                      decoration: InputDecoration(
                        hintText: 'Email_address',
                        hintStyle: TextStyle(color: Colors.black87, fontSize: 17),
                        focusColor: Colors.green,
                        focusedBorder: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(20),
                          borderSide: BorderSide(
                            color: Colors.pink,
                            width: 5,
                          ),
                        ),
                        enabledBorder: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(20),
                          borderSide: BorderSide(
                            color: Colors.grey,
                            width: 4,
                          ),
                        ),
                        suffixIcon: Icon(Icons.email, color: Colors.pink),
                      ),
                    ),
                    SizedBox(height: 10),
                    TextField(
                      controller: passwordController,
                      obscureText: true,
                      obscuringCharacter: '#',
                      cursorColor: Colors.lightBlueAccent,
                      style: TextStyle(color: Colors.black87, fontSize: 17),
                      decoration: InputDecoration(
                        hintText: 'Password',
                        hintStyle: TextStyle(color: Colors.black87, fontSize: 17),
                        focusedBorder: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(20),
                          borderSide: BorderSide(
                            color: Colors.pink,
                            width: 5,
                          ),
                        ),
                        enabledBorder: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(20),
                          borderSide: BorderSide(
                            color: Colors.grey,
                            width: 4,
                          ),
                        ),
                        suffixIcon: Icon(Icons.password_outlined, color: Colors.pink),
                      ),
                    ),
                    SizedBox(height: 10),
                    ElevatedButton(
                      onPressed: signUp,
                      child: Text("Sign Up"),
                    ),
                    SizedBox(height: 10),
                    Center(
                      child: Row(
                        mainAxisAlignment: MainAxisAlignment.center,
                      ),
                    ),
                  ],
                ),
              ),
              Container(
                padding: EdgeInsets.only(left: 30, right: 10),
                child: Row(
                  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                  children: [
                    TextButton(
                      onPressed: () {
                        _auth.createUserWithEmailAndPassword(
                            email: emailController.text.toString(),
                            password: passwordController.text.toString());
                        Navigator.push(context, MaterialPageRoute(
                            builder: (context) => imageLogin()),
                        );
                      },
                      child: Text(
                        "log In",
                        style: TextStyle(
                          color: Colors.white,
                          fontSize: 19,
                          fontWeight: FontWeight.w600,
                          decoration: TextDecoration.underline,
                          decorationColor: Colors.white,
                          decorationThickness: 1.6,
                        ),
                      ),
                    ),
                    TextButton(
                      onPressed: () {},
                      child: Text(
                        "Forgot Password",
                        style: TextStyle(
                          color: Colors.white,
                          fontSize: 19,
                          fontWeight: FontWeight.w600,
                          decoration: TextDecoration.underline,
                          decorationColor: Colors.white,
                          decorationThickness: 1.6,
                        ),
                      ),
                    ),
                  ],
                ),
              ),
              SizedBox(height: 0.2),
            ],
          ),
        ),
      ),
    );
  }
}
