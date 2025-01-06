import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(home: Scaffold(body: MyForm())));

class MyForm extends StatefulWidget {
  @override
  _MyFormState createState() => _MyFormState();
}

class _MyFormState extends State<MyForm> {
  final _formKey = GlobalKey<FormState>();
  final _nameController = TextEditingController(), _emailController = TextEditingController(), _passwordController = TextEditingController();
  bool _agreeToTerms = false;

  @override
  Widget build(BuildContext context) {
    return Form(
      key: _formKey,
      child: Column(
        children: [
          TextFormField(controller: _nameController, validator: (val) => val?.isEmpty ?? true ? 'Enter name' : null),
          TextFormField(controller: _emailController, validator: (val) => val?.isEmpty ?? true ? 'Enter email' : null),
          TextFormField(controller: _passwordController, obscureText: true, validator: (val) => val?.isEmpty ?? true ? 'Enter password' : null),
          Row(
            children: [
              Checkbox(value: _agreeToTerms, onChanged: (val) => setState(() => _agreeToTerms = val!)),
              Text('Agree to terms'),
            ],
          ),
          ElevatedButton(onPressed: () {
            if (_formKey.currentState?.validate() ?? false && _agreeToTerms) {
              ScaffoldMessenger.of(context).showSnackBar(SnackBar(content: Text('Form submitted')));
            }
          }, child: Text('Submit')),
        ],
      ),
    );
  }
}
