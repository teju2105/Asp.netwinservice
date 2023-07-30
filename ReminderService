# Asp.netwinservice

using System;
using System.Configuration;
using System.ServiceProcess;
using System.Timers;
using System.Net;
using System.Net.Mail;

namespace ReminderService
{
    public partial class ReminderService : ServiceBase
    {
        private Timer timer;

        public ReminderService()
        {
            InitializeComponent();
        }

        protected override void OnStart(string[] args)
        {
            // Set up the timer to trigger every 24 hours (you can adjust the interval as needed)
            timer = new Timer();
            timer.Interval = TimeSpan.FromHours(24).TotalMilliseconds;
            timer.Elapsed += Timer_Elapsed;
            timer.Start();
        }

        protected override void OnStop()
        {
            // Stop the timer when the service is stopped
            timer.Stop();
        }

        private void Timer_Elapsed(object sender, ElapsedEventArgs e)
        {
            // Trigger the reminder email sending logic here
            SendReminderEmail();
        }

        private void SendReminderEmail()
        {
            try
            {
                // Get email configuration from app settings
                string smtpServer = ConfigurationManager.AppSettings["SmtpServer"];
                int smtpPort = int.Parse(ConfigurationManager.AppSettings["SmtpPort"]);
                string smtpUsername = ConfigurationManager.AppSettings["SmtpUsername"];
                string smtpPassword = ConfigurationManager.AppSettings["SmtpPassword"];

                // Create the email message
                MailMessage message = new MailMessage();
                message.From = new MailAddress("sender@example.com");
                message.To.Add("recipient@example.com");
                message.Subject = "Reminder: Your Task";
                message.Body = "This is a reminder email for your task.";

                // Configure the SMTP client
                SmtpClient smtpClient = new SmtpClient(smtpServer, smtpPort);
                smtpClient.EnableSsl = true;
                smtpClient.Credentials = new NetworkCredential(smtpUsername, smtpPassword);

                // Send the email
                smtpClient.Send(message);
            }
            catch (Exception ex)
            {
                // Handle any exceptions or logging here
            }
        }
    }
}
