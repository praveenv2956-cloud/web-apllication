Chapter 1 — Web Application (In)security

TopicDescriptionEvolution of Web ApplicationsStarted as static pages; now handle banking, shopping, communication, etc.Common Web Application FunctionsLogin, search, file upload, payment, user profiles — common attack targetsBenefits of Web ApplicationsAccessible from anywhere, no installation needed, easy to updateThe Core Security ProblemUsers can type ANYTHING — attackers misuse this to send malicious inputKey Problem FactorsDevelopers trust user input, poor coding practices, lack of security testingThe New Security PerimeterTraditional firewalls are not enough; the web app itself must be securedFuture of Web App SecurityMore complex apps = more vulnerabilities; security must evolve continuously


Chapter 2 — Core Defense Mechanisms

TopicDescriptionAuthenticationVerifying who the user is (username/password, OTP, biometrics)Session ManagementServer tracks 
---user after login using session tokens/cookiesAccess ControlRestricting what authenticated users can do or accessBoundary ValidationValidate input at every layer — client-side AND server-sideHandling ErrorsNever show detailed error messages to users — attackers exploit themMaintaining Audit LogsRecord all important actions (login, data changes) for investigationAlerting AdministratorsAutomatically alert when suspicious activity is detectedReacting to AttacksBlock IPs, lock accounts, terminate sessions when an attack is detected


Chapter 3 — Web Application Technologies

TopicDescriptionHTTP Requests & ResponsesBrowser sends GET/POST requests; server replies with HTML/JSON + status codeHTTP MethodsGET, POST, PUT, DELETE, etc. — each used for different operationsCookies & Status CodesSmall browser-stored data to remember login state; codes like 200, 404, 500HTTPS & HTTP ProxiesHTTPS encrypts traffic; proxies intercept requests (used by hackers too)Server-Side FunctionalityPHP, Java, Python code running on server that processes requestsClient-Side FunctionalityJavaScript running in the browserEncoding (URL, Unicode, HTML, Base64)Different ways data is encoded while traveling over the internet


Chapter 4 — Mapping the Application

TopicDescriptionWeb SpideringAutomated tool crawls all pages to discover contentDiscovering Hidden ContentFinding pages not linked anywhere (admin panels, backup files)Identifying Entry PointsAll places where user input enters the app (forms, URL params, headers)Identifying Server-Side TechnologiesFinding out what language, framework, and database the app usesMapping the Attack SurfaceUnderstanding all possible points an attacker can target


Chapter 5 — Bypassing Client-Side Controls

TopicDescriptionHidden Form FieldsAttackers can change hidden values like price or user roleHTTP CookiesCookies can be modified by the user to change their privilegesURL ParametersValues like ?price=100 in URLs can be changed by attackersLength LimitsBrowser input length limits can be bypassed using a proxyScript-Based ValidationJavaScript validation on the browser side can be bypassed easilyDisabled ElementsDisabled buttons/fields can be re-enabled using browser developer toolsBrowser Extension InterceptionFlash/Java/Silverlight traffic can be intercepted and modified


Chapter 6 — Attacking Authentication

TopicDescriptionBad PasswordsWeak passwords like "123456" or "password" are easy to guessBrute-Force LoginAttacker tries thousands of passwords automatically until one worksVerbose Failure Messages"Username not found" vs "Wrong password" reveals too much informationCredential TransmissionSending credentials over HTTP (not HTTPS) allows interceptionPassword Change FunctionalityPoor implementation allows changing someone else's passwordForgotten Password FunctionalitySecurity questions or weak reset links can be exploitedRemember Me FunctionalityPersistent cookies can be stolen and reusedMultistage Login DefectsMulti-step login where steps can be skipped or reorderedInsecure StorageStoring passwords in plain text in a database is very dangerous


Chapter 7 — Attacking Session Management

TopicDescriptionMeaningful TokensTokens containing username or user ID can be decoded and guessedPredictable TokensTokens generated using time or sequence numbers can be predictedEncrypted TokensEven encrypted tokens can be vulnerable if encryption is weakToken Disclosure on NetworkTokens sent over HTTP can be captured by attackersToken Disclosure in LogsSession tokens appearing in server logs can be stolenVulnerable Session TerminationLogout doesn't properly destroy the session on the serverLiberal Cookie ScopeCookie set for entire domain can be accessed by subdomainsSession HijackingStealing another user's session token to access their account


Chapter 8 — Attacking Access Controls

TopicDescriptionUnprotected FunctionalityAdmin pages accessible without login (e.g., /admin/deleteuser)Identifier-Based FunctionsChanging ID in URL to access other users' data (e.g., ?userid=123)Multistage FunctionsSkipping steps in a multi-step process (e.g., skip payment, go to confirmation)Static FilesDirect URL access to files like PDFs or images that should be restrictedPlatform MisconfigurationServer misconfigured to allow access that should be blockedInsecure Access Control MethodsRelying on hidden URLs or referrer headers for security


Chapter 9 — Attacking Data Stores

TopicDescriptionSQL InjectionInserting malicious SQL code into input fields to manipulate the databaseBypassing LoginUsing SQL injection like ' OR '1'='1 to login without a passwordUNION OperatorUsing UNION in SQL injection to extract data from other tablesBypassing FiltersEncoding or modifying SQL to bypass input filtersSecond-Order SQL InjectionMalicious input stored in DB that is executed laterNoSQL Injection (MongoDB)Similar to SQL injection but targeting MongoDB databasesXPath InjectionInjecting into XML queries to extract unauthorized dataLDAP InjectionInjecting into LDAP directory queries to bypass authentication


Chapter 10 — Attacking Back-End Components

TopicDescriptionOS Command InjectionInjecting system commands through input fields (e.g., ; rm -rf /)Path TraversalUsing ../../../etc/passwd in file paths to access restricted filesFile Inclusion VulnerabilitiesMaking the app load a malicious file (local or remote)XML External Entities (XXE)Exploiting XML parsers to read local files or make server requestsSOAP InjectionManipulating SOAP XML messages to alter web service behaviorSMTP Command InjectionInjecting email headers to send spam or access other accounts


Chapter 11 — Attacking Application Logic

TopicDescriptionNature of Logic FlawsNot coding bugs, but flaws in how the application thinks/behavesFooling Password ChangeChanging another user's password by manipulating the requestProceeding to CheckoutSkipping payment step and going directly to order confirmationBreaking the BankTransferring a negative amount to increase your own balanceBeating a Business LimitBypassing limits like "max 5 coupons per user"Bulk Discount CheatingAdding items to get discount, then removing some itemsRace ConditionsTwo requests sent simultaneously to exploit timing issues (double spending)


Chapter 12 — Cross-Site Scripting (XSS)

TopicDescriptionReflected XSSMalicious script in URL is reflected back and executed in victim's browserStored XSSMalicious script saved in database; executes every time someone views the pageDOM-Based XSSScript executes due to unsafe JavaScript in the page itself (no server involved)XSS PayloadsSteal cookies, redirect users, keylog, deface websiteDelivery MechanismsSend malicious link via email, social media, or phishingPreventing XSSEncode output, use Content Security Policy (CSP), sanitize input


Chapter 13 — Attacking Users: Other Techniques

TopicDescriptionRequest Forgery (CSRF)Trick victim's browser into making unauthorized requests to another siteUI Redress (Clickjacking)Hide a malicious button under a legitimate-looking buttonHTML InjectionInject HTML tags to change page content and steal dataCSS InjectionInject CSS to capture user keystrokes or change page appearanceJavaScript HijackingSteal JSON data meant for another site using script tagsHTTP Header InjectionInject newlines into headers to add fake headers or redirectOpen RedirectionRedirect users to malicious sites using a trusted site's redirect parameterCookie InjectionInject values into cookies to manipulate application behavior


Chapter 14 — Automating Customized Attacks

TopicDescriptionEnumerating Valid IdentifiersAutomatically find valid usernames, order IDs, account numbersHarvesting Useful DataExtract useful information from multiple pages automaticallyFuzzingSend thousands of random/malformed inputs to find vulnerabilitiesBurp IntruderBurp Suite tool used to automate customized attacks with payloadsSession HandlingAutomatically refresh session tokens during long automated attacksCAPTCHA BypassTechniques to handle/bypass CAPTCHA during automation


Chapter 15 — Exploiting Information Disclosure

TopicDescriptionScript Error MessagesDetailed PHP/ASP errors reveal file paths and code structureStack TracesJava/.NET errors show internal function names and logicDebug MessagesDeveloper debug info left on in production reveals sensitive dataServer and Database MessagesMySQL/MSSQL errors reveal table names and column namesGathering Published InformationGoogle, Shodan, job listings reveal technology usedUsing InferenceGuess internal behavior from small clues in responses


Chapter 16 — Attacking Native Compiled Applications

TopicDescriptionStack OverflowOverwrite the call stack with too much data to hijack program executionHeap OverflowOverflow heap memory to corrupt data structuresOff-by-One VulnerabilityWriting one byte beyond a buffer boundary causes crash or exploitInteger OverflowNumber exceeds maximum size and wraps around to a small/negative valueSignedness ErrorsTreating a signed number as unsigned causes unexpected behaviorFormat String VulnerabilitiesPassing format strings like %x %x to read or write memory


Chapter 17 — Attacking Application Architecture

TopicDescriptionTiered ArchitecturesWeb apps have multiple tiers (web server, app server, DB server); compromising one exposes othersAttacking Tiered ArchitecturesMove laterally from web tier to database tierVirtual HostingMultiple sites on same server; misconfiguration can expose one site to anotherShared Application ServicesShared hosting means one customer's vulnerability affects othersAttacking Shared EnvironmentsExploit misconfiguration to access other customers' data


Chapter 18 — Attacking the Application Server

TopicDescriptionDefault CredentialsServers often have default admin/admin login that many forget to changeDefault ContentSample pages and test scripts left on the server can be exploitedDirectory ListingsServer shows all files in a folder when no index page existsWebDAV MethodsHTTP methods like PUT and DELETE enabled on server allow file uploadsApplication Server as ProxyMisconfigured server used to attack internal systemsWeb Application Firewalls (WAF)WAFs can be bypassed using encoding techniques


Chapter 19 — Finding Vulnerabilities in Source Code

TopicDescriptionBlack-Box vs White-Box TestingBlack-box = no source code access; White-box = full source code reviewSQL Injection SignaturesLook for mysql_query(), string concatenation with user inputXSS SignaturesLook for echo $_GET, document.write() without encodingPath TraversalLook for fopen() or include() using user-supplied filenamesOS Command InjectionLook for exec(), system(), shell_exec() with user inputJava Code ReviewDangerous APIs like Runtime.exec(), JDBC string concatenationPHP Code Revieweval(), include(), $_GET without sanitizationASP.NET Code ReviewResponse.Write(), SQL string building without parameters


Chapter 20 — Hacker's Toolkit

TopicDescriptionWeb BrowsersChrome/Firefox with developer tools for inspecting requests and responsesBurp SuiteMost popular tool for intercepting, modifying, and replaying HTTP requestsIntercepting ProxySits between browser and server to capture and modify all trafficVulnerability ScannersAutomated tools like Nikto and Acunetix to scan for known vulnerabilitiesLimitations of ScannersCannot find logic flaws; cannot understand business context


Chapter 21 — Web Application Hacker's Methodology

TopicDescriptionReconnaissanceGather info about the target (technologies, entry points, structure)Map the ApplicationSpider and manually browse to discover all functionalityTest All Entry PointsTest every input for injection, XSS, and access control issuesTest AuthenticationCheck for weak passwords, brute force, and session flawsTest AuthorizationCheck if users can access other users' dataTest Business LogicTry to bypass workflows, skip steps, and abuse featuresExploit and ReportDocument all findings with proof of concept and severity rating
