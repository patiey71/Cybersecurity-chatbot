# Cybersecurity-chatbot
// =====================================================================
//  CyberGuard Assistant - PROG6221 POE Part 2
//  HOW TO RUN:
//  1. Open Visual Studio 2022
//  2. File > New > Project > WPF Application (.NET 8)
//  3. Name it: CybersecurityChatbot
//  4. Replace ALL code in MainWindow.xaml.cs with this file
//  5. Replace ALL code in MainWindow.xaml with the XAML below
//  6. Press F5
// =====================================================================

// ============================
//  PASTE INTO: MainWindow.xaml
// ============================
/*
<Window x:Class="CybersecurityChatbot.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="CyberGuard - Cybersecurity Awareness Chatbot"
        Height="780" Width="960"
        MinHeight="600" MinWidth="700"
        Background="#0D1117"
        WindowStartupLocation="CenterScreen">

    <Window.Resources>
        <Style x:Key="BaseButton" TargetType="Button">
            <Setter Property="Foreground" Value="White"/>
            <Setter Property="FontWeight" Value="SemiBold"/>
            <Setter Property="FontSize" Value="13"/>
            <Setter Property="Padding" Value="20,10"/>
            <Setter Property="BorderThickness" Value="0"/>
            <Setter Property="Cursor" Value="Hand"/>
            <Setter Property="Template">
                <Setter.Value>
                    <ControlTemplate TargetType="Button">
                        <Border x:Name="Bd" Background="{TemplateBinding Background}"
                                CornerRadius="8" Padding="{TemplateBinding Padding}">
                            <ContentPresenter HorizontalAlignment="Center" VerticalAlignment="Center"/>
                        </Border>
                        <ControlTemplate.Triggers>
                            <Trigger Property="IsMouseOver" Value="True">
                                <Setter TargetName="Bd" Property="Opacity" Value="0.80"/>
                            </Trigger>
                            <Trigger Property="IsPressed" Value="True">
                                <Setter TargetName="Bd" Property="Opacity" Value="0.60"/>
                            </Trigger>
                        </ControlTemplate.Triggers>
                    </ControlTemplate>
                </Setter.Value>
            </Setter>
        </Style>
        <Style x:Key="BtnSend"  TargetType="Button" BasedOn="{StaticResource BaseButton}">
            <Setter Property="Background" Value="#1565C0"/>
        </Style>
        <Style x:Key="BtnHelp"  TargetType="Button" BasedOn="{StaticResource BaseButton}">
            <Setter Property="Background" Value="#2E7D32"/>
        </Style>
        <Style x:Key="BtnClear" TargetType="Button" BasedOn="{StaticResource BaseButton}">
            <Setter Property="Background" Value="#B71C1C"/>
        </Style>
    </Window.Resources>

    <Grid>
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="*"/>
            <RowDefinition Height="Auto"/>
        </Grid.RowDefinitions>

        <!-- HEADER -->
        <Border Grid.Row="0" Background="#0F3460" Padding="22,16">
            <Grid>
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="*"/>
                    <ColumnDefinition Width="Auto"/>
                </Grid.ColumnDefinitions>
                <StackPanel Grid.Column="0">
                    <TextBlock Text="🛡️  CyberGuard Assistant"
                               FontSize="26" FontWeight="Bold" Foreground="#EF5350"/>
                    <TextBlock Text="Your Cybersecurity Awareness Companion"
                               FontSize="12" Foreground="#90A4AE" Margin="0,5,0,0"/>
                </StackPanel>
                <StackPanel Grid.Column="1" Orientation="Horizontal" VerticalAlignment="Center">
                    <Ellipse Width="10" Height="10" Fill="#69F0AE" Margin="0,0,7,0"/>
                    <TextBlock Text="Online" Foreground="#69F0AE" FontSize="12" VerticalAlignment="Center"/>
                </StackPanel>
            </Grid>
        </Border>

        <!-- ASCII ART -->
        <Border Grid.Row="1" Background="#010409" Padding="10,8">
            <TextBlock x:Name="TxtAscii"
                       FontFamily="Courier New" FontSize="8"
                       Foreground="#00B0FF"
                       HorizontalAlignment="Center"
                       TextWrapping="Wrap"/>
        </Border>

        <!-- STATUS BAR -->
        <Border Grid.Row="2" Background="#161B22" Padding="18,7">
            <Grid>
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="*"/>
                    <ColumnDefinition Width="Auto"/>
                </Grid.ColumnDefinitions>
                <TextBlock x:Name="TxtStatus"
                           Text="💬  Type a message below to get started..."
                           Foreground="#6A737D" FontSize="12" VerticalAlignment="Center"/>
                <TextBlock x:Name="TxtTopic" Grid.Column="1"
                           Text="" Foreground="#00B0FF" FontSize="11" VerticalAlignment="Center"/>
            </Grid>
        </Border>

        <!-- CHAT DISPLAY -->
        <Border Grid.Row="3" Margin="14,10,14,6"
                Background="#0D1117" BorderBrush="#21262D"
                BorderThickness="1" CornerRadius="10">
            <ScrollViewer x:Name="Scroller"
                          VerticalScrollBarVisibility="Auto"
                          HorizontalScrollBarVisibility="Disabled"
                          Padding="6">
                <RichTextBox x:Name="ChatBox"
                             Background="Transparent" BorderThickness="0"
                             IsReadOnly="True" Foreground="White"
                             FontSize="13" Padding="10"
                             VerticalScrollBarVisibility="Disabled"
                             HorizontalScrollBarVisibility="Disabled"
                             FontFamily="Segoe UI"/>
            </ScrollViewer>
        </Border>

        <!-- INPUT AREA -->
        <Border Grid.Row="4" Background="#161B22" Padding="14,12">
            <Grid>
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="*"/>
                    <ColumnDefinition Width="Auto"/>
                    <ColumnDefinition Width="Auto"/>
                    <ColumnDefinition Width="Auto"/>
                </Grid.ColumnDefinitions>
                <Border Grid.Column="0" Background="#21262D" CornerRadius="8"
                        BorderBrush="#30363D" BorderThickness="1" Margin="0,0,10,0">
                    <TextBox x:Name="InputBox"
                             Background="Transparent" Foreground="White"
                             CaretBrush="White" FontSize="14"
                             Padding="14,10" BorderThickness="0"
                             VerticalAlignment="Center"
                             KeyDown="InputBox_KeyDown">
                        <TextBox.Resources>
                            <Style TargetType="Border">
                                <Setter Property="CornerRadius" Value="8"/>
                            </Style>
                        </TextBox.Resources>
                    </TextBox>
                </Border>
                <Button Grid.Column="1" Content="Send ▶"  Style="{StaticResource BtnSend}"
                        Click="BtnSend_Click"  Margin="0,0,8,0" VerticalAlignment="Center"/>
                <Button Grid.Column="2" Content="Help ?"  Style="{StaticResource BtnHelp}"
                        Click="BtnHelp_Click"  Margin="0,0,8,0" VerticalAlignment="Center"/>
                <Button Grid.Column="3" Content="Clear ✕" Style="{StaticResource BtnClear}"
                        Click="BtnClear_Click" VerticalAlignment="Center"/>
            </Grid>
        </Border>
    </Grid>
</Window>
*/

// ====================================
//  PASTE INTO: MainWindow.xaml.cs
// ====================================

using System;
using System.Collections.Generic;
using System.Linq;
using System.Windows;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;

namespace CybersecurityChatbot
{
    // ==================================================================
    //  ENUM — Sentiment types
    // ==================================================================
    public enum Sentiment { Neutral, Worried, Curious, Frustrated, Happy }

    // ==================================================================
    //  CLASS — UserMemory  (stores what the chatbot remembers)
    // ==================================================================
    public class UserMemory
    {
        public string       Name           { get; set; } = string.Empty;
        public string       FavouriteTopic { get; set; } = string.Empty;
        public List<string> TopicsAsked    { get; set; } = new List<string>();

        public bool HasName           => !string.IsNullOrWhiteSpace(Name);
        public bool HasFavouriteTopic => !string.IsNullOrWhiteSpace(FavouriteTopic);
    }

    // ==================================================================
    //  CLASS — ChatbotEngine  (all chatbot logic in one class)
    // ==================================================================
    public class ChatbotEngine
    {
        // ── Fields ────────────────────────────────────────────────────
        private readonly UserMemory _memory        = new UserMemory();
        private          string     _lastTopic     = string.Empty;
        private          bool       _awaitingName  = false;
        private          bool       _awaitingTopic = false;
        private readonly Random     _random        = new Random();

        // ── Topic keyword → list of responses (random pick each time) ─
        private readonly Dictionary<string, List<string>> _topicResponses
            = new Dictionary<string, List<string>>(StringComparer.OrdinalIgnoreCase)
        {
            ["password"] = new List<string>
            {
                "🔑 Use at least 12 characters mixing uppercase, lowercase, numbers and symbols.",
                "🔑 Never reuse the same password on different sites — use a password manager!",
                "🔑 Avoid personal details like your name or birthday in passwords.",
                "🔑 Change passwords immediately if you suspect an account has been compromised."
            },
            ["phishing"] = new List<string>
            {
                "🎣 Check the sender's email address carefully — phishing emails use look-alike domains.",
                "🎣 Never click links in unexpected emails. Go directly to the website instead.",
                "🎣 Legitimate organisations will never ask for your password via email.",
                "🎣 Hover over links before clicking to preview the real destination URL."
            },
            ["scam"] = new List<string>
            {
                "⚠️ If an offer sounds too good to be true, it almost certainly is!",
                "⚠️ Never send money or gift cards to someone you have not met in person.",
                "⚠️ Always verify the identity of anyone requesting sensitive personal information.",
                "⚠️ Report scams to your local consumer protection authority immediately."
            },
            ["privacy"] = new List<string>
            {
                "🔒 Review your social media privacy settings regularly.",
                "🔒 Limit the personal information you share publicly online.",
                "🔒 Read app permission requests carefully before granting access.",
                "🔒 Use a privacy-focused browser extension to block trackers."
            },
            ["malware"] = new List<string>
            {
                "🦠 Keep your antivirus software updated at all times.",
                "🦠 Only download software from official, reputable sources.",
                "🦠 Scan your device regularly for threats.",
                "🦠 Be cautious with USB drives from unknown sources."
            },
            ["ransomware"] = new List<string>
            {
                "💾 Back up important data regularly to an offline location.",
                "💾 Keep your operating system and software fully patched.",
                "💾 Never pay the ransom — it does not guarantee file recovery."
            },
            ["firewall"] = new List<string>
            {
                "🧱 Always keep your device firewall enabled.",
                "🧱 A router hardware firewall protects every device on the network.",
                "🧱 Review firewall logs occasionally to spot unusual connections."
            },
            ["2fa"] = new List<string>
            {
                "📱 Enable 2FA — it stops most account takeover attacks.",
                "📱 Use an authenticator app instead of SMS for stronger 2FA.",
                "📱 Enable 2FA on all accounts, starting with email and banking."
            },
            ["vpn"] = new List<string>
            {
                "🌐 A VPN encrypts your internet traffic on public Wi-Fi.",
                "🌐 Choose a reputable paid VPN — free ones often sell your data.",
                "🌐 A VPN hides your IP but does not make you fully anonymous."
            },
            ["social engineering"] = new List<string>
            {
                "🎭 Social engineering targets people, not systems — always verify requests.",
                "🎭 Pause and question any urgent or unusual request.",
                "🎭 Report suspicious communications to your security team."
            },
            ["data breach"] = new List<string>
            {
                "📊 Change passwords immediately on any account affected by a breach.",
                "📊 Check haveibeenpwned.com to see if your email has been exposed.",
                "📊 Enable breach alerts with your password manager."
            },
            ["encryption"] = new List<string>
            {
                "🔐 Enable full-disk encryption on your laptop to protect stolen data.",
                "🔐 Always look for HTTPS before entering sensitive information online.",
                "🔐 Encryption scrambles data so only authorised parties can read it."
            }
        };

        // ── Sentiment keyword lists ────────────────────────────────────
        private readonly List<string> _worriedWords    = new List<string>
            { "worried","scared","afraid","anxious","nervous","concern","fear","terrified","stress" };
        private readonly List<string> _frustratedWords = new List<string>
            { "frustrated","annoyed","angry","hate","useless","confusing","don't understand","not working" };
        private readonly List<string> _happyWords      = new List<string>
            { "great","awesome","love","thanks","thank you","helpful","amazing","perfect","excellent" };
        private readonly List<string> _curiousWords    = new List<string>
            { "curious","wonder","interested","how does","what is","tell me","explain","how do","why is" };

        // ── Other trigger lists ────────────────────────────────────────
        private readonly List<string> _followUpPhrases = new List<string>
            { "another tip","tell me more","explain more","more please","give me more",
              "continue","go on","what else","next tip","another one","keep going","more info" };
        private readonly List<string> _greetingWords   = new List<string>
            { "hello","hi","hey","greetings","good morning","good afternoon","good evening","howdy" };
        private readonly List<string> _goodbyeWords    = new List<string>
            { "bye","goodbye","exit","quit","see you","farewell","take care","later" };

        // ==============================================================
        //  PUBLIC — GetResponse  (main method called by the GUI)
        // ==============================================================
        public string GetResponse(string userInput)
        {
            if (string.IsNullOrWhiteSpace(userInput))
                return "Please type something so I can help you! 😊";

            string input = userInput.Trim();
            string lower = input.ToLower();

            // ── Collecting name ────────────────────────────────────────
            if (_awaitingName)
            {
                _awaitingName        = false;
                _memory.Name         = CapFirst(input.Split(' ')[0]);
                _awaitingTopic       = true;
                return $"Nice to meet you, {_memory.Name}! 😊\n\n" +
                       "What is your favourite cybersecurity topic?\n" +
                       "(e.g. passwords, phishing, privacy, malware…)";
            }

            // ── Collecting favourite topic ─────────────────────────────
            if (_awaitingTopic)
            {
                _awaitingTopic         = false;
                _memory.FavouriteTopic = input;
                return $"Got it, {_memory.Name}! I will remember that you are interested in " +
                       $"'{_memory.FavouriteTopic}'.\n" +
                       "It is a crucial part of staying safe online. 🛡️\n\n" +
                       "Feel free to ask me anything! Type 'help' to see all topics.";
            }

            // ── Greeting ───────────────────────────────────────────────
            if (_greetingWords.Any(w => lower.Contains(w)))
                return HandleGreeting();

            // ── Name introduction ──────────────────────────────────────
            if (lower.Contains("my name is") || lower.StartsWith("i am ")
                || lower.StartsWith("i'm ") || lower.StartsWith("call me "))
                return HandleNameIntro(input);

            // ── Help menu ──────────────────────────────────────────────
            if (lower.Contains("help") || lower.Contains("menu")
                || lower.Contains("topics") || lower.Contains("what can you do"))
                return ShowHelpMenu();

            // ── Follow-up (continue last topic) ───────────────────────
            if (_followUpPhrases.Any(p => lower.Contains(p)))
                return HandleFollowUp();

            // ── Memory recall: name ────────────────────────────────────
            if (lower.Contains("my name") || lower.Contains("what's my name"))
                return _memory.HasName
                    ? $"Of course! You told me your name is {_memory.Name}. 😊"
                    : "I do not know your name yet. Say 'My name is ...' and I will remember!";

            // ── Memory recall: favourite topic ─────────────────────────
            if (lower.Contains("my favourite") || lower.Contains("my favorite")
                || lower.Contains("what do i like"))
                return _memory.HasFavouriteTopic
                    ? $"You told me your favourite topic is '{_memory.FavouriteTopic}'! " +
                      "Would you like a tip about it?"
                    : "I do not know your favourite topic yet. What are you most interested in?";

            // ── Goodbye ────────────────────────────────────────────────
            if (_goodbyeWords.Any(w => lower.Contains(w)))
                return HandleGoodbye();

            // ── Sentiment detection ────────────────────────────────────
            Sentiment mood   = DetectSentiment(lower);
            string    prefix = SentimentPrefix(mood);

            // ── Keyword matching → random response from list ───────────
            foreach (KeyValuePair<string, List<string>> entry in _topicResponses)
            {
                if (lower.Contains(entry.Key.ToLower()))
                {
                    _lastTopic = entry.Key;
                    if (!_memory.TopicsAsked.Contains(entry.Key))
                        _memory.TopicsAsked.Add(entry.Key);

                    string tip = entry.Value[_random.Next(entry.Value.Count)];
                    return prefix + tip + MemoryNote(entry.Key);
                }
            }

            // ── Default / error handling ───────────────────────────────
            return DefaultResponse();
        }

        // ── Greeting handler ──────────────────────────────────────────
        private string HandleGreeting()
        {
            if (_memory.HasName)
                return $"Hello again, {_memory.Name}! 👋\n" +
                       "How can I help you with cybersecurity today?";
            _awaitingName = true;
            return "Hello! 👋 Welcome to CyberGuard Assistant.\n" +
                   "I am here to help you stay safe online.\n\nWhat is your name?";
        }

        // ── Name introduction handler ──────────────────────────────────
        private string HandleNameIntro(string input)
        {
            string[] patterns = { "my name is ", "i am ", "i'm ", "call me " };
            string name = input;
            foreach (string p in patterns)
            {
                int idx = input.ToLower().IndexOf(p);
                if (idx >= 0)
                {
                    name = input.Substring(idx + p.Length).Trim().TrimEnd('.','!',',','?');
                    break;
                }
            }
            _memory.Name   = CapFirst(name.Split(' ')[0]);
            _awaitingTopic = true;
            return $"Nice to meet you, {_memory.Name}! 😊\n\n" +
                   "What is your favourite cybersecurity topic?\n" +
                   "(e.g. passwords, phishing, privacy, malware…)";
        }

        // ── Follow-up handler ──────────────────────────────────────────
        private string HandleFollowUp()
        {
            if (string.IsNullOrEmpty(_lastTopic))
                return "Sure! Which topic would you like more on?\n" +
                       "Try: passwords, phishing, scam, privacy, malware, or type 'help'.";
            if (_topicResponses.ContainsKey(_lastTopic))
            {
                List<string> tips = _topicResponses[_lastTopic];
                return $"Here is another tip about {_lastTopic}:\n\n" +
                       tips[_random.Next(tips.Count)];
            }
            return DefaultResponse();
        }

        // ── Goodbye handler ────────────────────────────────────────────
        private string HandleGoodbye()
        {
            string name = _memory.HasName ? $", {_memory.Name}" : string.Empty;
            return $"Goodbye{name}! 👋 Stay safe online.\n\n" +
                   "Quick reminders:\n" +
                   "  • Keep all software updated\n" +
                   "  • Use strong, unique passwords\n" +
                   "  • Think before you click! 🛡️";
        }

        // ── Help menu ──────────────────────────────────────────────────
        private string ShowHelpMenu() =>
            "🛡️  Topics I can help you with:\n\n" +
            "  🔑  password           — Password safety\n"      +
            "  🎣  phishing           — Phishing attacks\n"      +
            "  ⚠️  scam              — Online scams\n"           +
            "  🔒  privacy            — Online privacy\n"         +
            "  🦠  malware            — Malware and viruses\n"   +
            "  💾  ransomware         — Ransomware defence\n"    +
            "  🧱  firewall           — Firewall basics\n"        +
            "  📱  2fa                — Two-factor auth\n"        +
            "  🌐  vpn                — VPN usage\n"             +
            "  🎭  social engineering — Social engineering\n"    +
            "  📊  data breach        — Data breaches\n"         +
            "  🔐  encryption         — Encryption basics\n\n"   +
            "Just type any keyword or ask a question!";

        // ── Default response (randomised) ──────────────────────────────
        private string DefaultResponse()
        {
            var list = new List<string>
            {
                "I am not sure I understand. Can you try rephrasing? 🤔",
                "Hmm, I did not catch that. Try asking about a cybersecurity topic.",
                "I am not familiar with that. Type 'help' to see what I can assist with.",
                "That is outside my expertise. Ask me about passwords, phishing, or privacy!"
            };
            return list[_random.Next(list.Count)];
        }

        // ── Sentiment detection ────────────────────────────────────────
        public Sentiment DetectSentiment(string lower)
        {
            if (_worriedWords.Any(w    => lower.Contains(w))) return Sentiment.Worried;
            if (_frustratedWords.Any(w => lower.Contains(w))) return Sentiment.Frustrated;
            if (_happyWords.Any(w      => lower.Contains(w))) return Sentiment.Happy;
            if (_curiousWords.Any(w    => lower.Contains(w))) return Sentiment.Curious;
            return Sentiment.Neutral;
        }

        private string SentimentPrefix(Sentiment mood)
        {
            switch (mood)
            {
                case Sentiment.Worried:
                    return "It is completely understandable to feel that way. " +
                           "You are already doing the right thing by learning about it! 💪\n\n";
                case Sentiment.Frustrated:
                    return "I understand this can be frustrating. " +
                           "Let me explain it as clearly as possible! 😊\n\n";
                case Sentiment.Curious:
                    return "Great question — I love your curiosity! " +
                           "Here is what you need to know:\n\n";
                case Sentiment.Happy:
                    return "Glad you are feeling positive! Here is a helpful tip:\n\n";
                default:
                    return string.Empty;
            }
        }

        // ── Memory personalisation note ────────────────────────────────
        private string MemoryNote(string topic)
        {
            if (_memory.HasFavouriteTopic &&
                _memory.FavouriteTopic.IndexOf(topic, StringComparison.OrdinalIgnoreCase) >= 0)
                return $"\n\n💡 As someone interested in {_memory.FavouriteTopic}, " +
                       "you might also want to review your account security settings!";

            if (_memory.HasName && _memory.TopicsAsked.Count >= 2)
            {
                List<string> last2 = _memory.TopicsAsked.TakeLast(2).ToList();
                return $"\n\n💡 {_memory.Name}, since you have been exploring " +
                       $"{last2[0]} and {last2[1]}, " +
                       "consider doing a full security check-up on your accounts!";
            }
            return string.Empty;
        }

        // ── Utility ────────────────────────────────────────────────────
        private static string CapFirst(string s)
            => string.IsNullOrEmpty(s) ? s : char.ToUpper(s[0]) + s.Substring(1).ToLower();

        public static string GetAsciiArt() =>
            " ██████╗██╗   ██╗██████╗ ███████╗██████╗      ██████╗ ██╗   ██╗ █████╗ ██████╗ ██████╗ \n" +
            "██╔════╝╚██╗ ██╔╝██╔══██╗██╔════╝██╔══██╗    ██╔════╝ ██║   ██║██╔══██╗██╔══██╗██╔══██╗\n" +
            "██║      ╚████╔╝ ██████╔╝█████╗  ██████╔╝    ██║  ███╗██║   ██║███████║██████╔╝██║  ██║\n" +
            "██║       ╚██╔╝  ██╔══██╗██╔══╝  ██╔══██╗    ██║   ██║██║   ██║██╔══██║██╔══██╗██║  ██║\n" +
            "╚██████╗   ██║   ██████╔╝███████╗██║  ██║    ╚██████╔╝╚██████╔╝██║  ██║██║  ██║██████╔╝\n" +
            " ╚═════╝   ╚═╝   ╚═════╝ ╚══════╝╚═╝  ╚═╝     ╚═════╝  ╚═════╝╚═╝  ╚═╝╚═╝  ╚═╝╚═════╝ ";
    }

    // ==================================================================
    //  CLASS — MainWindow  (WPF GUI code-behind)
    // ==================================================================
    public partial class MainWindow : Window
    {
        private readonly ChatbotEngine _engine = new ChatbotEngine();

        // Colour brushes
        private static readonly SolidColorBrush ColBot   = new SolidColorBrush(Color.FromRgb(0,   176, 255));
        private static readonly SolidColorBrush ColUser  = new SolidColorBrush(Color.FromRgb(239,  83,  80));
        private static readonly SolidColorBrush ColBotTx = new SolidColorBrush(Color.FromRgb(200, 220, 255));
        private static readonly SolidColorBrush ColUsrTx = new SolidColorBrush(Colors.White);
        private static readonly SolidColorBrush ColTime  = new SolidColorBrush(Color.FromRgb(100, 115, 130));
        private static readonly SolidColorBrush ColDiv   = new SolidColorBrush(Color.FromRgb(25,   38,  60));

        // ── Constructor ────────────────────────────────────────────────
        public MainWindow()
        {
            InitializeComponent();
            TxtAscii.Text = ChatbotEngine.GetAsciiArt();
            PlayVoice();
            BotSay("Hello! 👋 Welcome to CyberGuard Assistant.\n" +
                   "I am here to help you stay safe online.\n\nWhat is your name?");
        }

        // ── Voice greeting ─────────────────────────────────────────────
        private static void PlayVoice()
        {
            try
            {
                var s = new System.Speech.Synthesis.SpeechSynthesizer();
                s.Volume = 80;
                s.Rate   = -1;
                s.SpeakAsync("Welcome to CyberGuard Assistant. I am ready to help you stay safe online.");
            }
            catch { /* TTS not available — fail silently */ }
        }

        // ── Button clicks ──────────────────────────────────────────────
        private void BtnSend_Click(object sender, RoutedEventArgs e)  => Process();
        private void BtnHelp_Click(object sender, RoutedEventArgs e)  => Process("help");
        private void BtnClear_Click(object sender, RoutedEventArgs e)
        {
            ChatBox.Document.Blocks.Clear();
            TxtStatus.Text = "🗑️  Chat cleared.";
            TxtTopic.Text  = string.Empty;
            BotSay("Chat cleared! Ask me anything about cybersecurity. 🛡️");
        }
        private void InputBox_KeyDown(object sender, KeyEventArgs e)
        { if (e.Key == Key.Enter) Process(); }

        // ── Core process method ────────────────────────────────────────
        private void Process(string? text = null)
        {
            string input = text ?? InputBox.Text.Trim();
            if (string.IsNullOrEmpty(input)) return;

            UserSay(input);
            InputBox.Clear();
            InputBox.Focus();

            string response = _engine.GetResponse(input);
            BotSay(response);

            TxtStatus.Text = $"💬  Last message at {DateTime.Now:HH:mm:ss}";

            // Show recognised topic label
            string lower = input.ToLower();
            string[] topics = { "password","phishing","scam","privacy","malware",
                                 "ransomware","firewall","2fa","vpn","social engineering",
                                 "data breach","encryption" };
            string hit = topics.FirstOrDefault(t => lower.Contains(t)) ?? string.Empty;
            TxtTopic.Text = hit.Length > 0 ? $"📌  Topic: {hit}" : string.Empty;

            Scroller.ScrollToBottom();
        }

        // ── Chat display helpers ───────────────────────────────────────
        private void UserSay(string text) =>
            Append("You",            text, ColUser,  ColUsrTx, TextAlignment.Right);
        private void BotSay(string text)  =>
            Append("🛡️ CyberGuard", text, ColBot,   ColBotTx, TextAlignment.Left);

        private void Append(string sender, string text,
                            SolidColorBrush labelCol, SolidColorBrush textCol,
                            TextAlignment align)
        {
            var doc = ChatBox.Document;

            // Sender + timestamp
            var h = new Paragraph { Margin = new Thickness(0, 10, 0, 0), TextAlignment = align };
            h.Inlines.Add(new Run(sender + "   ")
                { Foreground = labelCol, FontWeight = FontWeights.Bold, FontSize = 13 });
            h.Inlines.Add(new Run(DateTime.Now.ToString("HH:mm"))
                { Foreground = ColTime, FontSize = 10 });
            doc.Blocks.Add(h);

            // Message body
            var b = new Paragraph { Margin = new Thickness(0, 3, 0, 0), TextAlignment = align };
            b.Inlines.Add(new Run(text) { Foreground = textCol, FontSize = 13 });
            doc.Blocks.Add(b);

            // Divider
            var d = new Paragraph { Margin = new Thickness(0, 5, 0, 0) };
            d.Inlines.Add(new Run(new string('─', 80)) { Foreground = ColDiv, FontSize = 9 });
            doc.Blocks.Add(d);
        }
    }
}
