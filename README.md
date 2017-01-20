# MVCLog4Netsample
Log4net
Step1: Please use Nuget to get Log4Net
enter image description here

Step2: Adding string

log4net.Config.XmlConfigurator.Configure();
in Global.asax.cs enter image description here

Step3: Adding another two sections A: First section

  <section name="log4net" type="log4net.Config.Log4NetConfigurationSectionHandler, log4net" />
in Web.Config between tag <configSections>...</configSections>

enter image description here

B:Second section, please insert into as following code in <configuration>...</configuration>

<log4net debug="true">
    <appender name="RollingLogFileAppender" type="log4net.Appender.RollingFileAppender">
      <file value="logs\log.txt" />
      <appendToFile value="true" />
      <rollingStyle value="Size" />
      <maxSizeRollBackups value="10" />
      <maximumFileSize value="100KB" />
      <staticLogFileName value="true" />
      <layout type="log4net.Layout.PatternLayout">
        <conversionPattern value="%-5p %d %5rms %-22.22c{1} %-18.18M - %m%n" />
      </layout>
    </appender>
    <root>
      <level value="DEBUG" />
      <appender-ref ref="RollingLogFileAppender" />
    </root>
  </log4net>
enter image description here

Final: Please insert as following code to any controller pages that you want to save log

private static log4net.ILog Log { get; set; }
  ILog log = log4net.LogManager.GetLogger(typeof(AccountController));      

        public ActionResult Index()
        {
            log.Debug("Debug message");
            log.Warn("Warn message");
            log.Error("Error message");
            log.Fatal("Fatal message");
            ViewBag.Title = "Home Page";
            return View();
        }
