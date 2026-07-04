#!/usr/bin/env python3
"""
Phishing Awareness Simulation Tool - Educational Cybersecurity Training
"""

import random
import sys

class PhishingAwarenessTool:
    """Educational tool for phishing awareness training"""
    
    def __init__(self):
        self.phishing_examples = {
            'urgent': {
                'name': 'Urgency/Threat',
                'example': """
Subject: URGENT: Your Account Will Be Suspended
    
Dear Customer, suspicious activity detected. Your account will be 
suspended in 24 hours unless you verify immediately.
Click: http://fake-bank-verify.com
""",
                'indicators': ['Urgent language', 'Generic greeting', 
                              'Suspicious link', 'Threat of account closure']
            },
            'spoofing': {
                'name': 'Email Spoofing',
                'example': """
Subject: Amazon Order #XY-23456
From: service@amaz0n-support.com

Your order is delayed. Update payment: http://amaz0n-secure.com
""",
                'indicators': ['Suspicious sender domain', 'Request for payment',
                              'Spoofed company name', 'Urgent action required']
            },
            'baiting': {
                'name': 'Baiting',
                'example': """
Subject: You Won a Free iPhone!

Congratulations! Claim your prize: http://free-iphone-winners.com
""",
                'indicators': ['Too-good-to-be-true offer', 'Unsolicited prize',
                              'Request for personal info', 'Suspicious domain']
            }
        }
        
        self.red_flags = [
            '• Suspicious sender email address (check domain carefully)',
            '• Urgency or threats to force immediate action',
            '• Requests for sensitive information (passwords, credit cards)',
            '• Too-good-to-be-true offers',
            '• Poor grammar and spelling errors',
            '• Generic greetings instead of your name',
            '• Suspicious links (hover to check destination)',
            '• Unexpected attachments'
        ]
        
    def display_menu(self):
        """Display main menu"""
        print("\n" + "="*60)
        print("  PHISHING AWARENESS TOOL")
        print("="*60)
        print("\n1. View Phishing Examples")
        print("2. Learn Red Flags")
        print("3. Take Quiz")
        print("4. Exit")
        print("-"*60)
        
    def view_examples(self):
        """Show phishing examples"""
        print("\n" + "="*60)
        print("  PHISHING EXAMPLES")
        print("="*60)
        
        for key, data in self.phishing_examples.items():
            print(f"\n📧 {data['name'].upper()}:")
            print("-"*40)
            print(data['example'])
            print("\n⚠️ Red Flags:")
            for flag in data['indicators']:
                print(f"  • {flag}")
            print("-"*40)
            input("Press Enter to continue...")
            
    def show_red_flags(self):
        """Display phishing red flags"""
        print("\n" + "="*60)
        print("  PHISHING RED FLAGS")
        print("="*60)
        print("\nWatch for these warning signs:\n")
        for flag in self.red_flags:
            print(flag)
        print("\n💡 Remember: Always verify through official channels!")
        print("="*60)
        input("\nPress Enter to continue...")
        
    def generate_quiz(self):
        """Generate and run quiz"""
        print("\n" + "="*60)
        print("  PHISHING QUIZ")
        print("="*60)
        print("\nIdentify if each is a phishing attempt (Y/N)")
        print("You'll get 5 questions.")
        input("\nPress Enter to start...")
        
        score = 0
        total = 5
        
        for i in range(total):
            # Pick random example
            key = random.choice(list(self.phishing_examples.keys()))
            example = self.phishing_examples[key]
            
            # 50% chance to show legitimate version
            if random.choice([True, False]):
                email = self.generate_legitimate()
                is_phishing = False
                explanation = "This appears legitimate. No urgency or suspicious elements."
            else:
                email = example['example']
                is_phishing = True
                explanation = f"This is phishing! {example['name']} tactic used."
            
            print(f"\n📧 Question {i+1}/{total}:")
            print("-"*40)
            print(email)
            print("-"*40)
            
            # Get user answer
            while True:
                answer = input("\nIs this phishing? (Y/N): ").strip().upper()
                if answer in ['Y', 'N']:
                    break
                print("Please enter Y or N")
            
            user_says_phishing = (answer == 'Y')
            
            if user_says_phishing == is_phishing:
                print("✅ Correct!")
                score += 1
            else:
                print("❌ Incorrect!")
            
            print(f"📚 {explanation}")
            if i < total - 1:
                input("\nPress Enter for next question...")
        
        # Show results
        print("\n" + "="*60)
        print(f"  QUIZ COMPLETE! Score: {score}/{total}")
        print("="*60)
        
        if score == total:
            print("\n🌟 Excellent! Great job spotting phishing!")
        elif score >= 4:
            print("\n👏 Good work! You're very aware!")
        elif score >= 3:
            print("\n📖 Good start! Review the examples to improve.")
        else:
            print("\n📚 Review the examples and red flags again.")
            
        print("\n💡 Always think before you click!")
        print("="*60)
        input("\nPress Enter to continue...")
        
    def generate_legitimate(self):
        """Generate a legitimate-looking email"""
        templates = [
            """
Subject: Your Account Status
From: security@yourbank.com

Your account is in good standing. No action needed.
Contact us at (800) 555-0123 with questions.
""",
            """
Subject: Order Confirmation
From: orders@amazon.com

Your order has been shipped! Track it through your account.
Thank you for shopping with us.
""",
            """
Subject: Newsletter
From: newsletter@tech.com

Your weekly tech news is ready to read.
Visit our website for the latest updates.
"""
        ]
        return random.choice(templates)
        
    def run(self):
        """Main application loop"""
        print("\n" + "="*60)
        print("  WELCOME TO PHISHING AWARENESS")
        print("="*60)
        print("\n⚠️  EDUCATIONAL USE ONLY")
        print("No actual phishing is conducted.\n")
        
        while True:
            self.display_menu()
            choice = input("\nEnter choice (1-4): ").strip()
            
            if choice == '1':
                self.view_examples()
            elif choice == '2':
                self.show_red_flags()
            elif choice == '3':
                self.generate_quiz()
            elif choice == '4':
                print("\n👋 Stay safe online!")
                break
            else:
                print("Invalid choice. Please enter 1-4.")

def main():
    try:
        tool = PhishingAwarenessTool()
        tool.run()
    except KeyboardInterrupt:
        print("\n\n👋 Goodbye!")
        sys.exit(0)

if __name__ == "__main__":
    main()# OptimusAutomate_PhishingAwarenessSimulationTool
