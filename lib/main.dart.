import 'dart:async';
import 'package:flutter/material.dart';
import 'package:shared_preferences/shared_preferences.dart';

void main() => runApp(const XyrooApp());

const red = Color(0xFFE53935);
const ink = Color(0xFF101621);
const bg = Color(0xFFE9EEF5);

class XyrooApp extends StatelessWidget {
  const XyrooApp({super.key});
  @override
  Widget build(BuildContext context) => MaterialApp(
    debugShowCheckedModeBanner: false,
    title: 'XYROO BUG',
    theme: ThemeData(useMaterial3: true, scaffoldBackgroundColor: bg,
      colorScheme: ColorScheme.fromSeed(seedColor: red)),
    home: const LoginScreen(),
  );
}

class LoginScreen extends StatefulWidget {
  const LoginScreen({super.key});
  @override State<LoginScreen> createState() => _LoginScreenState();
}
class _LoginScreenState extends State<LoginScreen> {
  final user = TextEditingController();
  final pass = TextEditingController();
  String error = '';
  bool loading = false;
  static const duration = Duration(hours: 1);

  Future<void> login() async {
    if (user.text.trim() != 'xyroo' || pass.text != '100911') {
      setState(() => error = 'Username atau password salah.');
      return;
    }
    setState(() { error = ''; loading = true; });
    final prefs = await SharedPreferences.getInstance();
    await prefs.setInt('xyrooLogin', DateTime.now().millisecondsSinceEpoch);
    if (!mounted) return;
    await Future.delayed(const Duration(milliseconds: 700));
    if (!mounted) return;
    Navigator.of(context).pushReplacement(MaterialPageRoute(
      builder: (_) => const HomeScreen()));
  }
  @override
  void dispose() { user.dispose(); pass.dispose(); super.dispose(); }
  @override
  Widget build(BuildContext context) => Scaffold(
    body: Stack(fit: StackFit.expand, children: [
      const AnimatedBackdrop(),
      Container(color: Colors.black.withOpacity(.25)),
      Center(child: SingleChildScrollView(padding: const EdgeInsets.all(20),
        child: Container(width: 370, padding: const EdgeInsets.all(22),
          decoration: BoxDecoration(color: Colors.white.withOpacity(.10),
            border: Border.all(color: ink, width: 5),
            borderRadius: BorderRadius.circular(28),
            boxShadow: const [BoxShadow(color: ink, offset: Offset(0, 8))]),
          child: Column(mainAxisSize: MainAxisSize.min, children: [
            Container(width: 72, height: 72, alignment: Alignment.center,
              decoration: BoxDecoration(color: ink, borderRadius: BorderRadius.circular(20)),
              child: const Text('X', style: TextStyle(color: red, fontSize: 42, fontWeight: FontWeight.w900))),
            const SizedBox(height: 14),
            const Text('XYROO', style: TextStyle(color: Colors.white, fontSize: 29, fontWeight: FontWeight.w900)),
            const SizedBox(height: 5),
            const Text('PREMIUM ACCESS PANEL', style: TextStyle(color: Colors.white70, fontSize: 12)),
            const SizedBox(height: 22),
            TextField(controller: user, style: const TextStyle(color: ink),
              decoration: fieldDecoration('Username')),
            const SizedBox(height: 12),
            TextField(controller: pass, obscureText: true, style: const TextStyle(color: ink),
              decoration: fieldDecoration('Password'),
              onSubmitted: (_) => login()),
            if (error.isNotEmpty) Padding(padding: const EdgeInsets.only(top: 12),
              child: Text(error, style: const TextStyle(color: Color(0xFFFFB4B4)))),
            const SizedBox(height: 18),
            SizedBox(width: double.infinity, child: ElevatedButton(
              style: redButton(), onPressed: loading ? null : login,
              child: Text(loading ? 'MEMUAT...' : 'LOGIN'))),
            const SizedBox(height: 10),
            const Text('Butuh bantuan akses? Hubungi administrator.',
              textAlign: TextAlign.center, style: TextStyle(color: Colors.white70, fontSize: 12)),
          ]),
        ),
      )),
    ]),
  );
}

InputDecoration fieldDecoration(String label) => InputDecoration(
  hintText: label, filled: true, fillColor: Colors.white.withOpacity(.88),
  contentPadding: const EdgeInsets.symmetric(horizontal: 14, vertical: 14),
  border: OutlineInputBorder(borderRadius: BorderRadius.circular(13),
    borderSide: const BorderSide(color: ink, width: 3)),
  enabledBorder: OutlineInputBorder(borderRadius: BorderRadius.circular(13),
    borderSide: const BorderSide(color: ink, width: 3)),
  focusedBorder: OutlineInputBorder(borderRadius: BorderRadius.circular(13),
    borderSide: const BorderSide(color: red, width: 3)),
);
ButtonStyle redButton() => ElevatedButton.styleFrom(
  backgroundColor: red, foregroundColor: Colors.white, elevation: 4,
  shadowColor: ink, side: const BorderSide(color: ink, width: 3),
  padding: const EdgeInsets.symmetric(vertical: 14),
  shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(14)),
  textStyle: const TextStyle(fontWeight: FontWeight.w900),
);

class AnimatedBackdrop extends StatefulWidget {
  const AnimatedBackdrop({super.key});
  @override State<AnimatedBackdrop> createState() => _AnimatedBackdropState();
}
class _AnimatedBackdropState extends State<AnimatedBackdrop> with SingleTickerProviderStateMixin {
  late final AnimationController controller = AnimationController(vsync: this, duration: const Duration(seconds: 7))..repeat();
  @override void dispose() { controller.dispose(); super.dispose(); }
  @override Widget build(BuildContext context) => AnimatedBuilder(animation: controller,
    builder: (_, __) => CustomPaint(painter: BackdropPainter(controller.value)));
}
class BackdropPainter extends CustomPainter {
  final double t;
  BackdropPainter(this.t);
  @override void paint(Canvas canvas, Size size) {
    canvas.drawRect(Offset.zero & size, Paint()..shader=const LinearGradient(
      colors: [Color(0xFF090D16), Color(0xFF2D374B), Color(0xFF180D12)],
      begin: Alignment.topLeft, end: Alignment.bottomRight).createShader(Offset.zero & size));
    final paint = Paint()..color = red.withOpacity(.15)..style = PaintingStyle.stroke..strokeWidth = 2;
    for (int i=0;i<6;i++) {
      final x = (size.width * ((i*.19 + t*.25) % 1));
      canvas.drawCircle(Offset(x, size.height*(.18 + (i%3)*.3)), 35 + (i%3)*22, paint);
    }
    final grid = Paint()..color = Colors.white.withOpacity(.06)..strokeWidth = 1;
    for(double x=0;x<size.width;x+=30) canvas.drawLine(Offset(x,0),Offset(x,size.height),grid);
    for(double y=0;y<size.height;y+=30) canvas.drawLine(Offset(0,y),Offset(size.width,y),grid);
  }
  @override bool shouldRepaint(covariant BackdropPainter oldDelegate) => oldDelegate.t != t;
}

class HomeScreen extends StatefulWidget {
  const HomeScreen({super.key});
  @override State<HomeScreen> createState() => _HomeScreenState();
}
class _HomeScreenState extends State<HomeScreen> {
  int tab = 0, keyCount = 50;
  String mode = 'CRASH';
  final target = TextEditingController();
  final key = TextEditingController();
  Timer? expiry;
  @override void initState() { super.initState(); _startExpiry(); _loadCount(); }
  Future<void> _loadCount() async {
    final p = await SharedPreferences.getInstance();
    if (mounted) setState(() => keyCount = p.getInt('xyrooKeyLimit') ?? 50);
  }
  Future<void> _startExpiry() async {
    final p = await SharedPreferences.getInstance();
    final saved = p.getInt('xyrooLogin');
    if (saved == null) { _logout(); return; }
    final remaining = const Duration(hours: 1).inMilliseconds -
      (DateTime.now().millisecondsSinceEpoch - saved);
    if (remaining <= 0) { await _logout(); return; }
    expiry = Timer(Duration(milliseconds: remaining), _logout);
  }
  Future<void> _logout() async {
    expiry?.cancel();
    final p = await SharedPreferences.getInstance();
    await p.remove('xyrooLogin');
    if (!mounted) return;
    Navigator.of(context).pushAndRemoveUntil(
      MaterialPageRoute(builder: (_) => const LoginScreen()), (_) => false);
    ScaffoldMessenger.of(context).showSnackBar(const SnackBar(content: Text('Sesi login berakhir. Silakan login kembali.')));
  }
  @override void dispose() { expiry?.cancel(); target.dispose(); key.dispose(); super.dispose(); }

  void notice(String title, String message) => showDialog<void>(context: context,
    builder: (_) => AlertDialog(title: Text(title), content: Text(message),
      shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(20)),
      actions: [TextButton(onPressed: () => Navigator.pop(context), child: const Text('OK'))]));

  Future<void> runSimulation() async {
    if (target.text.trim().isEmpty) { notice('TARGET REQUIRED', 'Masukkan nomor uji terlebih dahulu.'); return; }
    if (key.text.trim() != 'XYROO-NEW') { notice('ACCESS DENIED', 'Access key salah.'); return; }
    if (keyCount <= 0) { notice('KEY HABIS', 'Batas simulasi sudah habis.'); return; }
    setState(() => keyCount--);
    final p = await SharedPreferences.getInstance();
    await p.setInt('xyrooKeyLimit', keyCount);
    if (!mounted) return;
    showDialog<void>(context: context, builder: (_) => AlertDialog(
      title: const Text('SIMULASI SELESAI'),
      content: Text('Mode: $mode\\nNomor uji: ${target.text.trim()}\\nSisa key: $keyCount\\n\\nSimulasi lokal saja — tidak ada pesan eksternal yang dikirim.'),
      actions: [TextButton(onPressed: () => Navigator.pop(context), child: const Text('OK'))]));
  }

  @override Widget build(BuildContext context) {
    final pages = [
      _dashboard(), _whatsapp(), _notifications(), _tools(), _explore()
    ];
    return Scaffold(
      body: SafeArea(child: IndexedStack(index: tab, children: pages)),
      bottomNavigationBar: NavigationBar(
        selectedIndex: tab, onDestinationSelected: (i) => setState(() => tab=i),
        indicatorColor: red.withOpacity(.15),
        destinations: const [
          NavigationDestination(icon: Icon(Icons.home_outlined), label: 'DASH'),
          NavigationDestination(icon: Icon(Icons.chat_bubble_outline), label: 'WHATSAPP'),
          NavigationDestination(icon: Icon(Icons.notifications_none), label: 'NOTIFY'),
          NavigationDestination(icon: Icon(Icons.settings_outlined), label: 'TOOLS'),
          NavigationDestination(icon: Icon(Icons.explore_outlined), label: 'EXPLORE'),
        ]),
    );
  }

  Widget _shell(String title, String subtitle, List<Widget> children) => ListView(
    padding: const EdgeInsets.fromLTRB(16, 18, 16, 25),
    children: [
      Row(children: [Expanded(child: Text(title, style: const TextStyle(fontSize: 24, fontWeight: FontWeight.w900))),
        const Icon(Icons.circle, color: Color(0xFF43C77A), size: 10), const SizedBox(width: 5),
        const Text('ONLINE', style: TextStyle(fontSize: 10, fontWeight: FontWeight.bold))]),
      Padding(padding: const EdgeInsets.only(top: 4, bottom: 18), child: Text(subtitle, style: const TextStyle(color: Color(0xFF667085), fontSize: 12))),
      ...children,
    ]);
  Widget _card(Widget child) => Container(margin: const EdgeInsets.only(bottom: 15), padding: const EdgeInsets.all(17),
    decoration: BoxDecoration(color: Colors.white.withOpacity(.96), border: Border.all(color: ink, width: 3),
      borderRadius: BorderRadius.circular(20), boxShadow: const [BoxShadow(color: ink, offset: Offset(0,5))]), child: child);
  Widget _dashboard() => _shell('XYROO BUG', 'SYSTEM OVERVIEW', [
    Container(height: 270, margin: const EdgeInsets.only(bottom: 20), padding: const EdgeInsets.all(22),
      decoration: BoxDecoration(borderRadius: BorderRadius.circular(28), border: Border.all(color: ink, width: 4),
        gradient: const LinearGradient(colors: [Color(0xFF101621), Color(0xFF3A2734), Color(0xFF2D374B)], begin: Alignment.topLeft, end: Alignment.bottomRight),
        boxShadow: const [BoxShadow(color: ink, offset: Offset(0,7))]),
      child: Column(crossAxisAlignment: CrossAxisAlignment.start, mainAxisAlignment: MainAxisAlignment.end, children: [
        const Text('PREMIUM TOOLS', style: TextStyle(color: Color(0xFFFF5252), fontWeight: FontWeight.w900, letterSpacing: 2)),
        const SizedBox(height: 5), const Text('XYROO', style: TextStyle(color: Colors.white, fontSize: 37, fontWeight: FontWeight.w900)),
        const Text('"Anda sopan, kami segan. Anda punya alasan, kita punya apk andalan" ⚡',
          style: TextStyle(color: Colors.white70, fontSize: 12)),
        const SizedBox(height: 16), SizedBox(width: double.infinity, child: ElevatedButton(
          style: redButton(), onPressed: () => setState(() => tab=1), child: const Text('START'))),
      ])),
    _card(Column(crossAxisAlignment: CrossAxisAlignment.start, children: [
      const Row(children: [Expanded(child: Text('SYSTEM STATUS', style: TextStyle(fontWeight: FontWeight.w900))), Chip(label: Text('READY'))]),
      const SizedBox(height: 8), const Text('PERFORMANCE  86%', style: TextStyle(fontSize: 12)),
      const SizedBox(height: 7), const LinearProgressIndicator(value: .86, color: red, backgroundColor: Color(0xFFDCE2EA)),
      const SizedBox(height: 15), const Row(children: [
        Expanded(child: _Stat(value:'48%', label:'CPU')), Expanded(child: _Stat(value:'66%', label:'MEMORY')), Expanded(child: _Stat(value:'14%', label:'NETWORK'))])
    ])),
    GridView.count(shrinkWrap: true, physics: const NeverScrollableScrollPhysics(), crossAxisCount: 2,
      mainAxisSpacing: 10, crossAxisSpacing: 10, childAspectRatio: 1.6,
      children: const [_Feature('⚡','CRASH','Process control'),_Feature('♻️','MULTI','Multi process'),
        _Feature('🚀','FAST','Fast execution'),_Feature('🛡️','ANTI','Protection'),
        _Feature('💎','PREMIUM','Premium tools'),_Feature('⌘','CONSOLE','Live monitor')]),
  ]);
  Widget _whatsapp() => _shell('WHATSAPP', 'Message testing panel — simulasi lokal', [
    _card(Column(crossAxisAlignment: CrossAxisAlignment.start, children: [
      const _Label('TARGET NUMBER / NOMOR UJI'),
      TextField(controller: target, keyboardType: TextInputType.phone, decoration: fieldDecoration('628xxxxxxxxxx')),
      const _Label('ACCESS KEY'),
      TextField(controller: key, obscureText: true, decoration: fieldDecoration('Masukkan access key')),
      const _Label('PROCESS MODE'),
      Wrap(spacing: 8, runSpacing: 8, children: ['CRASH','FREEZE','DELAY','LOOP'].map((m) =>
        ChoiceChip(label: Text(m), selected: mode==m, selectedColor: red.withOpacity(.2),
          onSelected: (_) => setState(() => mode=m))).toList()),
      const SizedBox(height: 16),
      Row(children: [const Expanded(child: Text('BATAS KEY', style: TextStyle(fontWeight: FontWeight.w900))),
        Text('$keyCount', style: const TextStyle(fontSize: 25, fontWeight: FontWeight.w900, color: red))]),
      const SizedBox(height: 14), SizedBox(width: double.infinity, child: ElevatedButton(
        style: redButton(), onPressed: runSimulation, child: const Text('JALANKAN SIMULASI'))),
      const SizedBox(height: 10), const Text('Mode ini hanya mensimulasikan proses di aplikasi. Tidak mengirim pesan atau menyerang akun.', style: TextStyle(fontSize: 11, color: Color(0xFF667085))),
    ]))
  ]);
  Widget _notifications() => _shell('NOTIFICATION', 'System activity', [
    _note(Icons.check_circle, 'System Ready', 'Panel XYROO berhasil dimuat.'),
    _note(Icons.bolt, 'Process Engine', 'Simulasi lokal siap digunakan.'),
    _note(Icons.circle, 'Connection', 'Antarmuka berada dalam status online.'),
  ]);
  Widget _note(IconData icon, String title, String body) => _card(Row(crossAxisAlignment: CrossAxisAlignment.start, children: [
    Container(padding: const EdgeInsets.all(12), decoration: BoxDecoration(color: red, borderRadius: BorderRadius.circular(12)),
      child: Icon(icon, color: Colors.white)),
    const SizedBox(width: 12), Expanded(child: Column(crossAxisAlignment: CrossAxisAlignment.start, children: [
      Text(title, style: const TextStyle(fontWeight: FontWeight.w900)), const SizedBox(height: 4),
      Text(body, style: const TextStyle(color: Color(0xFF667085), fontSize: 12))
    ]))
  ]));
  Widget _tools() => _shell('TOOLS', 'System configuration', [
    _tool('Auto Process','Automatic process control', false),
    _tool('Fast Mode','Increase process speed', false),
    _tool('Protection','Protection interface', true),
    _tool('Debug Console','Show process information', false),
  ]);
  Widget _tool(String title, String desc, bool initial) => _ToolCard(title: title, desc: desc, initial: initial);
  Widget _explore() => _shell('EXPLORE', 'XYROO information', [
    _exploreCard('⚡ CRASH','Antarmuka bergaya processing dengan status dan konfigurasi.'),
    _exploreCard('🚀 FAST','Animasi proses dibuat responsif agar tampilan terasa seperti panel processing.'),
    _exploreCard('🛡️ SAFE MODE','Semua fungsi proses dalam aplikasi ini hanya simulasi lokal.'),
  ]);
  Widget _exploreCard(String title, String body) => _card(Column(crossAxisAlignment: CrossAxisAlignment.start, children: [
    Text(title, style: const TextStyle(fontSize: 18, fontWeight: FontWeight.w900)),
    const SizedBox(height: 7), Text(body, style: const TextStyle(color: Color(0xFF667085), fontSize: 12, height: 1.5))
  ]));
}

class _Stat extends StatelessWidget {
  final String value, label;
  const _Stat({required this.value, required this.label});
  @override Widget build(BuildContext context) => Container(margin: const EdgeInsets.symmetric(horizontal: 3),
    padding: const EdgeInsets.symmetric(vertical: 12, horizontal: 4),
    decoration: BoxDecoration(border: Border.all(color: const Color(0xFFCCD3DE), width: 2), borderRadius: BorderRadius.circular(12)),
    child: Column(children: [Text(value, style: const TextStyle(fontSize: 18, fontWeight: FontWeight.w900)), Text(label, style: const TextStyle(fontSize: 10, color: Color(0xFF667085)))]));
}
class _Feature extends StatelessWidget {
  final String icon, title, sub;
  const _Feature(this.icon, this.title, this.sub);
  @override Widget build(BuildContext context) => Container(padding: const EdgeInsets.all(13),
    decoration: BoxDecoration(color: Colors.white, border: Border.all(color: ink, width: 3),
      borderRadius: BorderRadius.circular(16), boxShadow: const [BoxShadow(color: ink, offset: Offset(0,4))]),
    child: Column(crossAxisAlignment: CrossAxisAlignment.start, mainAxisAlignment: MainAxisAlignment.center, children: [
      Text(icon, style: const TextStyle(fontSize: 23)), Text(title, style: const TextStyle(fontWeight: FontWeight.w900)),
      Text(sub, style: const TextStyle(fontSize: 10, color: Color(0xFF667085)))
    ]));
}
class _Label extends StatelessWidget {
  final String text;
  const _Label(this.text);
  @override Widget build(BuildContext context) => Padding(padding: const EdgeInsets.only(top: 13, bottom: 6),
    child: Text(text, style: const TextStyle(fontSize: 11, fontWeight: FontWeight.w900)));
}
class _ToolCard extends StatefulWidget {
  final String title, desc;
  final bool initial;
  const _ToolCard({required this.title, required this.desc, required this.initial});
  @override State<_ToolCard> createState() => _ToolCardState();
}
class _ToolCardState extends State<_ToolCard> {
  late bool enabled = widget.initial;
  @override Widget build(BuildContext context) => Container(margin: const EdgeInsets.only(bottom: 12),
    padding: const EdgeInsets.all(15), decoration: BoxDecoration(color: Colors.white, border: Border.all(color: ink, width: 3), borderRadius: BorderRadius.circular(16)),
    child: SwitchListTile(contentPadding: EdgeInsets.zero, activeColor: red, value: enabled,
      onChanged: (v) => setState(() => enabled=v), title: Text(widget.title, style: const TextStyle(fontWeight: FontWeight.w900)),
      subtitle: Text(widget.desc, style: const TextStyle(fontSize: 11))));
}
