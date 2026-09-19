# mande-africa
Application mobile et web MANDÉ AFRICA - Services financiers numériques
lib/
├── main.dart
├── theme/
│   └── app_theme.dart
├── screens/
│   ├── splash_screen.dart
│   ├── login_screen.dart
│   ├── home_screen.dart
│   ├── payment_screen.dart
│   ├── transfer_screen.dart
│   ├── recharge_screen.dart
│   ├── history_screen.dart
│   └── profile_screen.dart
└── widgets/
    ├── mande_logo.dart
    └── service_card.dart
name: mande_africa
description: Application financière numérique MANDÉ AFRICA
publish_to: "none"

version: 1.0.0+1

environment:
  sdk: ">=3.0.0 <4.0.0"

dependencies:
  flutter:
    sdk: flutter

  cupertino_icons: ^1.0.8

dev_dependencies:
  flutter_test:
    sdk: flutter

  flutter_lints: ^5.0.0

flutter:
  uses-material-design: true
  flutter pub get
  import 'package:flutter/material.dart';

import 'screens/splash_screen.dart';
import 'theme/app_theme.dart';

void main() {
  WidgetsFlutterBinding.ensureInitialized();

  runApp(const MandeAfricaApp());
}

class MandeAfricaApp extends StatelessWidget {
  const MandeAfricaApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'MANDÉ AFRICA',
      theme: AppTheme.light,
      home: const SplashScreen(),
    );
  }
}
lib/theme
app_theme.dart
import 'package:flutter/material.dart';

class AppTheme {
  static const Color primary = Color(0xFF0B6B3A);
  static const Color secondary = Color(0xFFD4A72C);
  static const Color dark = Color(0xFF101828);
  static const Color background = Color(0xFFF7F8FA);

  static ThemeData get light {
    return ThemeData(
      useMaterial3: true,
      scaffoldBackgroundColor: background,

      colorScheme: ColorScheme.fromSeed(
        seedColor: primary,
        primary: primary,
        secondary: secondary,
      ),

      appBarTheme: const AppBarTheme(
        backgroundColor: Colors.white,
        foregroundColor: dark,
        elevation: 0,
        centerTitle: false,
      ),

      inputDecorationTheme: InputDecorationTheme(
        filled: true,
        fillColor: Colors.white,
        border: OutlineInputBorder(
          borderRadius: BorderRadius.circular(14),
          borderSide: BorderSide.none,
        ),
        enabledBorder: OutlineInputBorder(
          borderRadius: BorderRadius.circular(14),
          borderSide: BorderSide.none,
        ),
        focusedBorder: OutlineInputBorder(
          borderRadius: BorderRadius.circular(14),
          borderSide: const BorderSide(
            color: primary,
            width: 1.5,
          ),
        ),
      ),

      elevatedButtonTheme: ElevatedButtonThemeData(
        style: ElevatedButton.styleFrom(
          backgroundColor: primary,
          foregroundColor: Colors.white,
          minimumSize: const Size(double.infinity, 54),
          shape: RoundedRectangleBorder(
            borderRadius: BorderRadius.circular(14),
          ),
        ),
      ),
    );
  }
}
lib/widgets/mande_logo.dart
import 'package:flutter/material.dart';

class MandeLogo extends StatelessWidget {
  final double size;

  const MandeLogo({
    super.key,
    this.size = 70,
  });

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisSize: MainAxisSize.min,
      children: [
        Container(
          width: size,
          height: size,
          decoration: BoxDecoration(
            color: const Color(0xFF0B6B3A),
            borderRadius: BorderRadius.circular(20),
          ),
          child: const Icon(
            Icons.account_balance_wallet,
            color: Colors.white,
            size: 38,
          ),
        ),

        const SizedBox(height: 10),

        const Text(
          'MANDÉ',
          style: TextStyle(
            fontSize: 22,
            fontWeight: FontWeight.bold,
            letterSpacing: 2,
            color: Color(0xFF0B6B3A),
          ),
        ),

        const Text(
          'AFRICA',
          style: TextStyle(
            fontSize: 13,
            fontWeight: FontWeight.w600,
            letterSpacing: 4,
            color: Color(0xFFD4A72C),
          ),
        ),
      ],
    );
  }
}
lib/screens/splash_screen.dart
import 'dart:async';

import 'package:flutter/material.dart';

import '../widgets/mande_logo.dart';
import 'login_screen.dart';

class SplashScreen extends StatefulWidget {
  const SplashScreen({super.key});

  @override
  State<SplashScreen> createState() => _SplashScreenState();
}

class _SplashScreenState extends State<SplashScreen> {
  @override
  void initState() {
    super.initState();

    Timer(
      const Duration(seconds: 3),
      () {
        if (!mounted) return;

        Navigator.pushReplacement(
          context,
          MaterialPageRoute(
            builder: (_) => const LoginScreen(),
          ),
        );
      },
    );
  }

  @override
  Widget build(BuildContext context) {
    return const Scaffold(
      backgroundColor: Colors.white,
      body: Center(
        child: MandeLogo(
          size: 85,
        ),
      ),
    );
  }
}
lib/screens/login_screen.dart
import 'package:flutter/material.dart';

import 'home_screen.dart';
import '../widgets/mande_logo.dart';

class LoginScreen extends StatefulWidget {
  const LoginScreen({super.key});

  @override
  State<LoginScreen> createState() => _LoginScreenState();
}

class _LoginScreenState extends State<LoginScreen> {
  final phoneController = TextEditingController();
  final passwordController = TextEditingController();

  bool obscurePassword = true;

  @override
  void dispose() {
    phoneController.dispose();
    passwordController.dispose();
    super.dispose();
  }

  void login() {
    Navigator.pushReplacement(
      context,
      MaterialPageRoute(
        builder: (_) => const HomeScreen(),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SafeArea(
        child: SingleChildScrollView(
          padding: const EdgeInsets.all(24),
          child: Column(
            children: [
              const SizedBox(height: 35),

              const MandeLogo(
                size: 75,
              ),

              const SizedBox(height: 45),

              const Align(
                alignment: Alignment.centerLeft,
                child: Text(
                  'Bienvenue sur MANDÉ AFRICA',
                  style: TextStyle(
                    fontSize: 25,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),

              const SizedBox(height: 8),

              const Align(
                alignment: Alignment.centerLeft,
                child: Text(
                  'Connectez-vous à votre compte.',
                  style: TextStyle(
                    color: Colors.grey,
                    fontSize: 15,
                  ),
                ),
              ),

              const SizedBox(height: 30),

              TextField(
                controller: phoneController,
                keyboardType: TextInputType.phone,
                decoration: const InputDecoration(
                  labelText: 'Numéro de téléphone',
                  prefixIcon: Icon(Icons.phone),
                ),
              ),

              const SizedBox(height: 16),

              TextField(
                controller: passwordController,
                obscureText: obscurePassword,
                decoration: InputDecoration(
                  labelText: 'Mot de passe',
                  prefixIcon: const Icon(Icons.lock),
                  suffixIcon: IconButton(
                    onPressed: () {
                      setState(() {
                        obscurePassword = !obscurePassword;
                      });
                    },
                    icon: Icon(
                      obscurePassword
                          ? Icons.visibility
                          : Icons.visibility_off,
                    ),
                  ),
                ),
              ),

              const SizedBox(height: 12),

              Align(
                alignment: Alignment.centerRight,
                child: TextButton(
                  onPressed: () {},
                  child: const Text(
                    'Mot de passe oublié ?',
                  ),
                ),
              ),

              const SizedBox(height: 15),

              ElevatedButton(
                onPressed: login,
                child: const Text(
                  'SE CONNECTER',
                  style: TextStyle(
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),

              const SizedBox(height: 20),

              TextButton(
                onPressed: () {},
                child: const Text(
                  'Créer un compte',
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
lib/widgets/service_card.dart
import 'package:flutter/material.dart';

class ServiceCard extends StatelessWidget {
  final IconData icon;
  final String title;
  final String subtitle;
  final VoidCallback onTap;

  const ServiceCard({
    super.key,
    required this.icon,
    required this.title,
    required this.subtitle,
    required this.onTap,
  });

  @override
  Widget build(BuildContext context) {
    return InkWell(
      borderRadius: BorderRadius.circular(18),
      onTap: onTap,
      child: Container(
        padding: const EdgeInsets.all(18),
        decoration: BoxDecoration(
          color: Colors.white,
          borderRadius: BorderRadius.circular(18),
          boxShadow: [
            BoxShadow(
              color: Colors.black.withOpacity(0.05),
              blurRadius: 15,
              offset: const Offset(0, 5),
            ),
          ],
        ),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Container(
              width: 48,
              height: 48,
              decoration: BoxDecoration(
                color: const Color(0xFF0B6B3A).withOpacity(0.1),
                borderRadius: BorderRadius.circular(14),
              ),
              child: Icon(
                icon,
                color: const Color(0xFF0B6B3A),
              ),
            ),

            const SizedBox(height: 15),

            Text(
              title,
              style: const TextStyle(
                fontWeight: FontWeight.bold,
                fontSize: 16,
              ),
            ),

            const SizedBox(height: 5),

            Text(
              subtitle,
              style: const TextStyle(
                color: Colors.grey,
                fontSize: 12,
              ),
            ),
          ],
        ),
      ),
    );
  }
}
lib/screens/home_screen.dart
import 'package:flutter/material.dart';

import '../widgets/service_card.dart';
import 'payment_screen.dart';
import 'transfer_screen.dart';
import 'recharge_screen.dart';
import 'history_screen.dart';
import 'profile_screen.dart';

class HomeScreen extends StatefulWidget {
  const HomeScreen({super.key});

  @override
  State<HomeScreen> createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  int currentIndex = 0;

  final List<Widget> pages = const [
    HomeContent(),
    HistoryScreen(),
    ProfileScreen(),
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: pages[currentIndex],

      bottomNavigationBar: NavigationBar(
        selectedIndex: currentIndex,

        onDestinationSelected: (index) {
          setState(() {
            currentIndex = index;
          });
        },

        destinations: const [
          NavigationDestination(
            icon: Icon(Icons.home_outlined),
            selectedIcon: Icon(Icons.home),
            label: 'Accueil',
          ),
          NavigationDestination(
            icon: Icon(Icons.history_outlined),
            selectedIcon: Icon(Icons.history),
            label: 'Historique',
          ),
          NavigationDestination(
            icon: Icon(Icons.person_outline),
            selectedIcon: Icon(Icons.person),
            label: 'Profil',
          ),
        ],
      ),
    );
  }
}

class HomeContent extends StatelessWidget {
  const HomeContent({super.key});

  @override
  Widget build(BuildContext context) {
    return SafeArea(
      child: SingleChildScrollView(
        padding: const EdgeInsets.all(20),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Row(
              children: [
                const Expanded(
                  child: Column(
                    crossAxisAlignment: CrossAxisAlignment.start,
                    children: [
                      Text(
                        'Bonjour 👋',
                        style: TextStyle(
                          color: Colors.grey,
                        ),
                      ),
                      SizedBox(height: 4),
                      Text(
                        'Mamadou',
                        style: TextStyle(
                          fontSize: 24,
                          fontWeight: FontWeight.bold,
                        ),
                      ),
                    ],
                  ),
                ),

                CircleAvatar(
                  backgroundColor: const Color(0xFF0B6B3A),
                  child: const Icon(
                    Icons.person,
                    color: Colors.white,
                  ),
                ),
              ],
            ),

            const SizedBox(height: 25),

            Container(
              width: double.infinity,
              padding: const EdgeInsets.all(22),
              decoration: BoxDecoration(
                gradient: const LinearGradient(
                  colors: [
                    Color(0xFF0B6B3A),
                    Color(0xFF094D2B),
                  ],
                ),
                borderRadius: BorderRadius.circular(22),
              ),
              child: const Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Text(
                    'Solde disponible',
                    style: TextStyle(
                      color: Colors.white70,
                    ),
                  ),

                  SizedBox(height: 8),

                  Text(
                    '0 FCFA',
                    style: TextStyle(
                      color: Colors.white,
                      fontSize: 32,
                      fontWeight: FontWeight.bold,
                    ),
                  ),

                  SizedBox(height: 15),

                  Text(
                    'MANDÉ AFRICA',
                    style: TextStyle(
                      color: Colors.white70,
                      letterSpacing: 2,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                ],
              ),
            ),

            const SizedBox(height: 28),

            const Text(
              'Services',
              style: TextStyle(
                fontSize: 21,
                fontWeight: FontWeight.bold,
              ),
            ),

            const SizedBox(height: 15),

            GridView.count(
              crossAxisCount: 2,
              crossAxisSpacing: 15,
              mainAxisSpacing: 15,
              shrinkWrap: true,
              physics: const NeverScrollableScrollPhysics(),
              childAspectRatio: 1.15,
              children: [
                ServiceCard(
                  icon: Icons.send,
                  title: 'Transfert',
                  subtitle: 'Envoyer de l’argent',
                  onTap: () {
                    Navigator.push(
                      context,
                      MaterialPageRoute(
                        builder: (_) => const TransferScreen(),
                      ),
                    );
                  },
                ),

                ServiceCard(
                  icon: Icons.payment,
                  title: 'Paiement',
                  subtitle: 'Payer un service',
                  onTap: () {
                    Navigator.push(
                      context,
                      MaterialPageRoute(
                        builder: (_) => const PaymentScreen(),
                      ),
                    );
                  },
                ),

                ServiceCard(
                  icon: Icons.phone_android,
                  title: 'Recharge',
                  subtitle: 'Crédit téléphone',
                  onTap: () {
                    Navigator.push(
                      context,
                      MaterialPageRoute(
                        builder: (_) => const RechargeScreen(),
                      ),
                    );
                  },
                ),

                ServiceCard(
                  icon: Icons.history,
                  title: 'Historique',
                  subtitle: 'Voir les opérations',
                  onTap: () {
                    Navigator.push(
                      context,
                      MaterialPageRoute(
                        builder: (_) => const HistoryScreen(),
                      ),
                    );
                  },
                ),
              ],
            ),
          ],
        ),
      ),
    );
  }
}
lib/screens/transfer_screen.dart
import 'package:flutter/material.dart';

class TransferScreen extends StatefulWidget {
  const TransferScreen({super.key});

  @override
  State<TransferScreen> createState() => _TransferScreenState();
}

class _TransferScreenState extends State<TransferScreen> {
  final phoneController = TextEditingController();
  final amountController = TextEditingController();

  void sendMoney() {
    ScaffoldMessenger.of(context).showSnackBar(
      const SnackBar(
        content: Text(
          'Fonction de transfert en préparation.',
        ),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Transfert'),
      ),

      body: Padding(
        padding: const EdgeInsets.all(20),
        child: Column(
          children: [
            TextField(
              controller: phoneController,
              keyboardType: TextInputType.phone,
              decoration: const InputDecoration(
                labelText: 'Numéro du bénéficiaire',
                prefixIcon: Icon(Icons.phone),
              ),
            ),

            const SizedBox(height: 18),

            TextField(
              controller: amountController,
              keyboardType: TextInputType.number,
              decoration: const InputDecoration(
                labelText: 'Montant en FCFA',
                prefixIcon: Icon(Icons.money),
              ),
            ),

            const SizedBox(height: 30),

            ElevatedButton(
              onPressed: sendMoney,
              child: const Text('CONTINUER'),
            ),
          ],
        ),
      ),
    );
  }
}
lib/screens/payment_screen.dart
import 'package:flutter/material.dart';

class PaymentScreen extends StatelessWidget {
  const PaymentScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Paiement'),
      ),

      body: Padding(
        padding: const EdgeInsets.all(20),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            const Text(
              'Payer un service',
              style: TextStyle(
                fontSize: 24,
                fontWeight: FontWeight.bold,
              ),
            ),

            const SizedBox(height: 25),

            ListTile(
              leading: const CircleAvatar(
                child: Icon(Icons.qr_code),
              ),
              title: const Text('Paiement QR'),
              subtitle: const Text(
                'Scanner un code QR',
              ),
              trailing: const Icon(
                Icons.arrow_forward_ios,
                size: 16,
              ),
              onTap: () {},
            ),

            const Divider(),

            ListTile(
              leading: const CircleAvatar(
                child: Icon(Icons.store),
              ),
              title: const Text('Paiement marchand'),
              subtitle: const Text(
                'Payer un commerçant',
              ),
              trailing: const Icon(
                Icons.arrow_forward_ios,
                size: 16,
              ),
              onTap: () {},
            ),
          ],
        ),
      ),
    );
  }
}
lib/screens/recharge_screen.dart
import 'package:flutter/material.dart';

class RechargeScreen extends StatefulWidget {
  const RechargeScreen({super.key});

  @override
  State<RechargeScreen> createState() => _RechargeScreenState();
}

class _RechargeScreenState extends State<RechargeScreen> {
  final phoneController = TextEditingController();
  final amountController = TextEditingController();

  String operator = 'Orange Mali';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Recharge téléphone'),
      ),

      body: Padding(
        padding: const EdgeInsets.all(20),
        child: Column(
          children: [
            DropdownButtonFormField<String>(
              initialValue: operator,

              decoration: const InputDecoration(
                labelText: 'Opérateur',
              ),

              items: const [
                DropdownMenuItem(
                  value: 'Orange Mali',
                  child: Text('Orange Mali'),
                ),
                DropdownMenuItem(
                  value: 'Moov Africa',
                  child: Text('Moov Africa'),
                ),
                DropdownMenuItem(
                  value: 'Telecel',
                  child: Text('Telecel'),
                ),
              ],

              onChanged: (value) {
                if (value != null) {
                  setState(() {
                    operator = value;
                  });
                }
              },
            ),

            const SizedBox(height: 18),

            TextField(
              controller: phoneController,
              keyboardType: TextInputType.phone,
              decoration: const InputDecoration(
                labelText: 'Numéro',
                prefixIcon: Icon(Icons.phone),
              ),
            ),

            const SizedBox(height: 18),

            TextField(
              controller: amountController,
              keyboardType: TextInputType.number,
              decoration: const InputDecoration(
                labelText: 'Montant',
                prefixIcon: Icon(Icons.money),
              ),
            ),

            const SizedBox(height: 30),

            ElevatedButton(
              onPressed: () {},
              child: const Text('RECHARGER'),
            ),
          ],
        ),
      ),
    );
  }
}
lib/screens/history_screen.dart
import 'package:flutter/material.dart';

class HistoryScreen extends StatelessWidget {
  const HistoryScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Historique'),
      ),

      body: ListView(
        padding: const EdgeInsets.all(20),
        children: const [
          TransactionItem(
            icon: Icons.send,
            title: 'Transfert',
            date: 'Aucune opération',
            amount: '0 FCFA',
          ),

          TransactionItem(
            icon: Icons.phone_android,
            title: 'Recharge',
            date: 'Aucune opération',
            amount: '0 FCFA',
          ),
        ],
      ),
    );
  }
}

class TransactionItem extends StatelessWidget {
  final IconData icon;
  final String title;
  final String date;
  final String amount;

  const TransactionItem({
    super.key,
    required this.icon,
    required this.title,
    required this.date,
    required this.amount,
  });

  @override
  Widget build(BuildContext context) {
    return Card(
      margin: const EdgeInsets.only(bottom: 12),
      child: ListTile(
        leading: CircleAvatar(
          child: Icon(icon),
        ),
        title: Text(
          title,
          style: const TextStyle(
            fontWeight: FontWeight.bold,
          ),
        ),
        subtitle: Text(date),
        trailing: Text(
          amount,
          style: const TextStyle(
            fontWeight: FontWeight.bold,
          ),
        ),
      ),
    );
  }
}
lib/screens/profile_screen.dart
import 'package:flutter/material.dart';

class ProfileScreen extends StatelessWidget {
  const ProfileScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Mon profil'),
      ),

      body: ListView(
        padding: const EdgeInsets.all(20),
        children: [
          const CircleAvatar(
            radius: 45,
            backgroundColor: Color(0xFF0B6B3A),
            child: Icon(
              Icons.person,
              size: 50,
              color: Colors.white,
            ),
          ),

          const SizedBox(height: 15),

          const Center(
            child: Text(
              'Mamadou',
              style: TextStyle(
                fontSize: 22,
                fontWeight: FontWeight.bold,
              ),
            ),
          ),

          const SizedBox(height: 30),

          ListTile(
            leading: const Icon(Icons.person),
            title: const Text('Informations personnelles'),
            trailing: const Icon(Icons.chevron_right),
            onTap: () {},
          ),

          ListTile(
            leading: const Icon(Icons.security),
            title: const Text('Sécurité'),
            trailing: const Icon(Icons.chevron_right),
            onTap: () {},
          ),

          ListTile(
            leading: const Icon(Icons.notifications),
            title: const Text('Notifications'),
            trailing: const Icon(Icons.chevron_right),
            onTap: () {},
          ),

          ListTile(
            leading: const Icon(Icons.help),
            title: const Text('Aide'),
            trailing: const Icon(Icons.chevron_right),
            onTap: () {},
          ),

          const SizedBox(height: 20),

          OutlinedButton(
            onPressed: () {
              Navigator.pop(context);
            },
            child: const Text('SE DÉCONNECTER'),
          ),
        ],
      ),
    );
  }
}
flutter clean
flutter pub get
flutter run
flutter devices
                 MANDÉ AFRICA
                      ↓
                  SPLASH
                      ↓
                 CONNEXION
                      ↓
                  ACCUEIL
                      ↓
       ┌──────────────┼──────────────┐
       ↓              ↓              ↓
   TRANSFERT       PAIEMENT       RECHARGE
       │              │              │
       └──────────────┼──────────────┘
                      ↓
                  HISTORIQUE
                      ↓
                    PROFIL
                    Bonjour 👋
Mamadou

┌──────────────────────────┐
│ Solde disponible         │
│                          │
│ 0 FCFA                   │
│                          │
│ MANDÉ AFRICA             │
└──────────────────────────┘

Services

┌─────────────┐ ┌─────────────┐
│  ↗          │ │  💳         │
│ Transfert   │ │ Paiement    │
└─────────────┘ └─────────────┘

┌─────────────┐ ┌─────────────┐
│  📱         │ │  ↻          │
│ Recharge    │ │ Historique  │
└─────────────┘ └─────────────┘
MANDÉ AFRICA
     │
     ├── Flutter Android/iPhone
     │
     ├── API Backend
     │
     ├── Base de données
     │
     ├── Authentification
     │
     ├── Comptes utilisateurs
     │
     ├── Transactions
     │
     ├── Historique
     │
     └── Intégrations de paiement
