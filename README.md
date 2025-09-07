# EventSphere
** Digital Event Management Platform - Event Sphere: **

## Features
EventSphere is a modern, scalable event management platform with the following features:

### Event Management
- **Create, Edit, Delete Events:** Organizers can create new events, update details, and remove events as needed.
- **Event Details:**
   - Title, description, date/time
   - Venue/location (physical address or online link)
   - Category (Music, Tech, Health, Education, etc.)
   - Type: Online or Offline events
   - Paid or Free events
   - **Recurrence:** Support for one-time and recurring events (daily, weekly, monthly, custom)
- **Speakers & Media:** Add event speakers, upload images and videos, and manage event media galleries.
- **FAQs & Feedback:** Organizers can add FAQs for attendees, and users can submit feedback after events.
- **Event Invitations:** Send invitations to users and track responses.
- **Event Logs:** Track changes and actions performed on events for auditing.
- **Upcoming & Trending Events:** Users can browse upcoming and trending events, with dynamic filtering and sorting.
- **Advanced Filtering:**
   - Filter by category, type, location, paid/free, online/offline, recurrence, and more.

### Registration & Ticketing
- **User Registration:** Attendees can register for events and manage their registrations.
- **Ticket Generation & QR Code generation as well :** Automatic ticket creation with unique QR codes for validation at entry.

### Payments & Stripe Integration
- **Secure Payments:** Integrated with Stripe for secure payment processing.
- **Stripe Connect:** Organizers can onboard with Stripe Express to receive payouts directly.
- **Payment APIs:** Backend provides endpoints for creating payment intents and checkout sessions.
- **Webhook Listener:** Stripe webhooks are handled for real-time payment status updates.

### User & Organizer Management
- **Authentication:** Register, login, verify email, forgot/reset password flows.
- **Profile Management:** Users can update their profile, including uploading profile images.
- **Organizer Onboarding:** Organizers can connect their Stripe account and view onboarding status.
- **Role-Based Access:** Admins, organizers, and users have different permissions and dashboard views.
- **Organizer view of payments:** Organizers can see their individual event payment details like payment id and user who had payed for event. 

### Bookmarks & Notifications
- **Bookmark Events:** Users can bookmark favorite events for quick access.
- **Email Notifications:** Automated emails for registration, reminders, and organizer communications. Real-time notifications for event updates, payments, and reminders.

### Admin Dashboard
- **Event Approval:** Admins can approve or reject new events and event edits.
- **Payments & Income Summary:** View all event payments, refunds, and income reports.
- **User & Event Management:** Manage users, events, and monitor platform activity.

### Additional Features
- **Responsive Frontend:** Built with Next.js and Tailwind CSS for a modern, mobile-friendly UI.
- **Terms and Conditions:** Dedicated page for platform policies.
- **Custom Middleware:** Logging, error handling, rate limiting, and request validation for robust backend operations.
- **SMTP Email Integration:** Send transactional emails via SMTP.
- **API Documentation:** (If enabled) Swagger or similar documentation for backend APIs.
- **Automated Testing:** Backend includes unit and integration tests for reliability.
- **Uploads:** Support for event media uploads (images/videos) stored in `wwwroot/uploads`.

---

## Backend
### Backend Controllers & API Endpoints

#### AdminController (`/api/admin`)
- POST `/api/admin/register` — Register admin
- PUT `/api/admin/event/{id}/approve` — Approve event
- PUT `/api/admin/event-edit/{id}/approve` — Approve event edit
- GET `/api/admin/event/{eventId}/payments` — Get payments for event
- GET `/api/admin/payments` — Get all event payments
- GET `/api/admin/events` — Get all events
- GET `/api/admin/event-income-summary` — Get event income summary

#### AuthController (`/api/auth`)
- POST `/api/auth/register` — Register user
- POST `/api/auth/login` — Login
- GET `/api/auth/verify-email` — Verify email
- POST `/api/auth/forgot-password` — Forgot password
- POST `/api/auth/reset-password` — Reset password

#### BookmarksController (`/api/bookmarks`)
- POST `/api/bookmarks/add` — Add bookmark
- DELETE `/api/bookmarks/delete/{eventId}` — Delete bookmark
- GET `/api/bookmarks/bookmarked-events/{userId}` — Get bookmarked events

#### DashboardController (`/api/dashboard`)
- GET `/api/dashboard/organized-events-payments/{userId}` — Get organized events payments
- POST `/api/dashboard/current-organized/{id}` — Current organized events
- POST `/api/dashboard/past-organized/{id}` — Past organized events
- POST `/api/dashboard/current-attending/{id}` — Current attending events
- POST `/api/dashboard/past-attended/{id}` — Past attended events

#### EmailController (`/api/email`)
- POST `/api/email/send-to-organiser` — Send email to organiser

#### EventsController (`/api/events`)
- GET `/api/events` — Get all events
- GET `/api/events/{id}` — Get event by ID
- POST `/api/events` — Create event
- PUT `/api/events/{id}` — Update event
- DELETE `/api/events/{id}` — Delete event
- GET `/api/events/editeventcount/{id}` — Get edit event count

#### HomeController (`/api/home`)
- GET `/api/home/upcoming` — Get upcoming events
- GET `/api/home/trending` — Get trending events
- POST `/api/home/filter` — Filter events

#### NotificationsController (`/api/notifications`)
- GET `/api/notifications` — Get all notifications
- GET `/api/notifications/{id}` — Get notification by ID
- POST `/api/notifications` — Create notification
- PUT `/api/notifications/{id}` — Update notification
- DELETE `/api/notifications/{id}` — Delete notification

#### PaymentsController (`/api/payments`)
- POST `/api/payments/create-payment-intent` — Create payment intent
- POST `/api/payments/create-checkout-session` — Create checkout session
- POST `/api/payments/webhook` — Stripe webhook
- POST `/api/payments/confirm` — Confirm payment

#### RegistrationsController (`/api/registrations`)
- GET `/api/registrations` — Get all registrations
- GET `/api/registrations/{id}` — Get registration by ID
- POST `/api/registrations` — Create registration
- PUT `/api/registrations/{id}` — Update registration
- DELETE `/api/registrations/{id}` — Delete registration

#### TicketsController (`/api/tickets`)
- GET `/api/tickets` — Get all tickets
- GET `/api/tickets/{id}` — Get ticket by ID
- POST `/api/tickets` — Create ticket
- PUT `/api/tickets/{id}` — Update ticket
- DELETE `/api/tickets/{id}` — Delete ticket

#### UsersController (`/api/users`)
- GET `/api/users/{id}` — Get user by ID
- PUT `/api/users/{id}` — Update user
- DELETE `/api/users/{id}` — Delete user
- POST `/api/users/{id}/stripe-express-account` — Create Stripe Express account
- GET `/api/users/{id}/stripe-onboarding-status` — Get Stripe onboarding status


#### WebsiteReviewController (`/api/website-review`)
- POST `/api/website-review` — Submit a website review
- GET `/api/website-review` — Get all website reviews
- GET `/api/website-review/{id}` — Get a specific website review by ID
- DELETE `/api/website-review/{id}` — Delete a website review by ID

---

## Stripe Payments Integration

### Backend Setup

1. **Get Stripe API Keys**
   - Sign up at [Stripe](https://dashboard.stripe.com/register) and create a project.
   - Go to Developers > API keys and copy your **Secret Key** and **Publishable Key**.
   - Also enable Stripe Connect for the created account.

2. **Configure Stripe Keys**
   - Add your secret key to the `.env` file:
     ```
     STRIPE_SECRET_KEY=pk_testabckdfi
     ```

3. **Endpoints for Payments**
   - `POST /api/payments/create-payment-intent` — Creates a Stripe PaymentIntent.
   - `POST /api/payments/create-checkout-session` — Creates a Stripe Checkout session.
   - See `PaymentsController.cs` for usage and request/response formats.

4. **Testing Payments**
   - Use Stripe test cards (e.g., `4242 4242 4242 4242`, any future expiry, any CVC).
   - Stripe test mode does not charge real money.

### Frontend Setup

1. **Install Stripe and configure environment variables**
   - Install Stripe package in your frontend project.
   - Add Stripe keys to your environment variables as needed.

2. **Stripe Webhook Listener**
   - Run the following command to forward Stripe webhooks to your backend:
     ```
     stripe listen --forward-to http://localhost:5274/Payments/webhooks
     ```
   - This command should be running to process payment requests from Stripe.

### Stripe Dashboard
- Monitor payments, refunds, and test transactions at [dashboard.stripe.com](https://dashboard.stripe.com/).
- Switch between test and live mode as needed.

---

Every organizer needs to have their Stripe account ID connected. This is done by creating a Stripe Connect account and then connecting it to the organizer account.

## End-to-End Steps to Run the Project

### Prerequisites
- [.NET 8 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)
- [SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads) (or update connection string for your DB)
- [Node.js (v18+ recommended)](https://nodejs.org/)
- [npm](https://www.npmjs.com/) (comes with Node.js)

### 1. Clone the Repository
```sh
git clone <repo-url>
cd LTIM_DEMP_2_repo
```

### 2. Configure Environment Variables
- Add your Stripe secret key to `backend/.env`:
   ```
   STRIPE_SECRET_KEY=your_stripe_secret_key
   ```
- Edit `backend/appsettings.Development.json` and `backend/appsettings.json` for your SQL Server connection string, SMTP, and JWT key.

### 3. Restore Dependencies
- Backend:
   ```sh
   cd backend
   dotnet restore
   ```
- Frontend:
   ```sh
   cd ../frontend
   npm install
   ```

### 4. Apply Database Migrations
```sh
cd ../backend
dotnet ef database update --project project.csproj
```

### 5. Start Backend and Frontend Servers
- Backend:
   ```sh
   dotnet run --project project.csproj
   ```
   The API will be available at `https://localhost:5001` or `http://localhost:5274`.
- Frontend:
   ```sh
   cd ../frontend
   npm run dev
   ```
   The app will be available at [http://localhost:3000](http://localhost:3000).

### 6. Stripe Webhook Listener (for payments)
Run this in a separate terminal:
```sh
stripe listen --forward-to http://localhost:5274/Payments/webhooks
```

### 7. Single Command to Start Everything (Windows)
You can use the provided PowerShell script:
```sh
./start-dev.ps1
```
This will start both backend and frontend servers if configured in the script.

---

## Project Folder Structure

```text
LTIM_DEMP_2_repo/
├── backend/
│   ├── .env
│   ├── .github/
│   ├── .gitignore
│   ├── .vscode/
│   ├── appsettings.Development.json
│   ├── appsettings.json
│   ├── backend.sln
│   ├── EventSphere.API/
│   │   ├── appsettings.json
│   │   ├── Controllers/
│   │   │   ├── AdminController.cs
│   │   │   ├── AuthController.cs
│   │   │   ├── BookmarksController.cs
│   │   │   ├── DashboardController.cs
│   │   │   ├── EmailController.cs
│   │   │   ├── EventsController.cs
│   │   │   ├── HomeController.cs
│   │   │   ├── NotificationsController.cs
│   │   │   ├── PaymentsController.cs
│   │   │   ├── RegistrationsController.cs
│   │   │   ├── TicketsController.cs
│   │   │   ├── UsersController.cs
│   │   │   └── WebsiteReviewController.cs
│   │   ├── Helpers/
│   │   │   └── JsonModelBinder.cs
│   │   ├── Middleware/
│   │   │   ├── CustomMiddleware.cs
│   │   │   ├── ErrorHandlingMiddleware.cs
│   │   │   ├── JwtMiddleware.cs
│   │   │   ├── LoggingMiddleware.cs
│   │   │   ├── PerformanceLoggingMiddleware.cs
│   │   │   ├── RateLimitingMiddleware.cs
│   │   │   ├── RequestValidationMiddleware.cs
│   │   │   └── ResponseFormattingMiddleware.cs
│   │   └── Program.cs
│   ├── EventSphere.Application/
│   │   ├── Dtos/
│   │   │   ├── SendEmailDto.cs
│   │   │   ├── Auth/
│   │   │   │   ├── AdminRegisterDto.cs
│   │   │   │   ├── ForgotPasswordDto.cs
│   │   │   │   ├── ResetPasswordDto.cs
│   │   │   │   ├── UpdateUserProfileDto.cs
│   │   │   │   ├── UserDetailsDto.cs
│   │   │   │   ├── UserLoginDto.cs
│   │   │   │   └── UserRegisterDto.cs
│   │   │   ├── Events/
│   │   │   │   ├── ApiResponse.cs
│   │   │   │   ├── CreateEventDto.cs
│   │   │   │   ├── DashboardDto.cs
│   │   │   │   ├── EditEventDto.cs
│   │   │   │   ├── EventCardDto.cs
│   │   │   │   ├── EventDto.cs
│   │   │   │   ├── EventFaqDto.cs
│   │   │   │   ├── EventMediaDto.cs
│   │   │   │   ├── EventOccurrenceDto.cs
│   │   │   │   ├── EventSpeakerDto.cs
│   │   │   │   ├── OrganizedEventPaymentsDto.cs
│   │   │   │   ├── UpdateEventApiDto.cs
│   │   │   │   └── UpdateEventDto.cs
│   │   │   ├── Home/
│   │   │   │   ├── AddBookmarkDto.cs
│   │   │   │   ├── EventCardDto.cs
│   │   │   │   └── EventFilterDto.cs
│   │   │   ├── Notifications/
│   │   │   │   └── NotificationDto.cs
│   │   │   ├── Payments/
│   │   │   │   ├── CheckoutRequestDto.cs
│   │   │   │   ├── CheckoutSessionDtos.cs
│   │   │   │   ├── EventIncomeDto.cs
│   │   │   │   ├── PaymentConfirmationDto.cs
│   │   │   │   └── PaymentDtos.cs
│   │   │   └── Registrations/
│   │   │   │   └── RegistrationDtos.cs
│   │   ├── Helpers/
│   │   │   ├── AuthHelper.cs
│   │   │   ├── ConfigHelper.cs
│   │   │   ├── EventDtoHelper.cs
│   │   │   └── FileHelper.cs
│   │   ├── Interfaces/
│   │   │   ├── IAdminService.cs
│   │   │   ├── IBookmarkService.cs
│   │   │   ├── IDashboardService.cs
│   │   │   ├── IEventService.cs
│   │   │   ├── IHomeService.cs
│   │   │   ├── INotificationService.cs
│   │   │   ├── IPaymentService.cs
│   │   │   ├── IRegistrationService.cs
│   │   │   └── IUserService.cs
│   │   ├── Mappers/
│   │   │   ├── EventMapper.cs
│   │   │   └── UserMapper.cs
│   │   ├── Repositories/
│   │   │   ├── IAuthRepository.cs
│   │   │   ├── IBookmarkRepository.cs
│   │   │   ├── IEventRepository.cs
│   │   │   ├── IPaymentRepository.cs
│   │   │   ├── IRegistrationRepository.cs
│   │   │   ├── ITicketRepository.cs
│   │   │   └── RegistrationRepository.cs
│   │   └── Services/
│   │   │   ├── AdminService.cs
│   │   │   ├── BookmarkService.cs
│   │   │   ├── DashboardService.cs
│   │   │   ├── EventService.cs
│   │   │   ├── FileService.cs
│   │   │   ├── HomeService.cs
│   │   │   ├── HourlyEventCompletionService.cs
│   │   │   ├── HourlyEventReminderService.cs
│   │   │   ├── ITicketRepository.cs
│   │   │   ├── ITicketService.cs
│   │   │   ├── NotificationService.cs
│   │   │   ├── PaymentService.cs
│   │   │   ├── RegistrationService.cs
│   │   │   ├── ScheduledReminderService.cs
│   │   │   ├── TicketService.cs
│   │   │   └── UserService.cs
│   ├── EventSphere.Domain/
│   │   ├── Entities/
│   │   │   ├── Bookmark.cs
│   │   │   ├── EmailTemplate.cs
│   │   │   ├── Event.cs
│   │   │   ├── EventFaqs.cs
│   │   │   ├── EventFeedback.cs
│   │   │   ├── EventInvitation.cs
│   │   │   ├── EventLog.cs
│   │   │   ├── EventMedia.cs
│   │   │   ├── EventOccurrences.cs
│   │   │   ├── EventSpeaker.cs
│   │   │   ├── Notification.cs
│   │   │   ├── Payment.cs
│   │   │   ├── Registration.cs
│   │   │   ├── Ticket.cs
│   │   │   ├── User.cs
│   │   │   └── Waitlist.cs
│   │   └── Enums/
│   │   │   ├── EmailTemplateEnums.cs
│   │   │   ├── EventEnums.cs
│   │   │   ├── EventInvitationEnums.cs
│   │   │   ├── EventMediaEnums.cs
│   │   │   ├── NotificationEnums.cs
│   │   │   ├── PaymentEnums.cs
│   │   │   ├── RegistrationEnums.cs
│   │   │   ├── TicketEnums.cs
│   │   │   └── UserEnums.cs
│   ├── EventSphere.Infrastructure/
│   │   ├── Data/
│   │   │   ├── AppDbContext.cs
│   │   │   └── AppDbContextFactory.cs
│   │   ├── Helpers/
│   │   │   ├── JwtHelper.cs
│   │   │   └── SmtpEmailSender.cs
│   │   ├── Migrations/
│   │   │   └── 20250727_FixIdentityColumns.cs
│   │   └── Repositories/
│   │   │   ├── AuthRepository.cs
│   │   │   ├── BookmarkRepository.cs
│   │   │   ├── EventRepository.cs
│   │   │   ├── PaymentRepository.cs
│   │   │   ├── RegistrationRepository.cs
│   │   │   └── TicketRepository.cs
│   ├── EventSphere.Tests/
│   │   ├── Controllers/
│   │   ├── Dtos/
│   │   ├── Entities/
│   │   ├── Helpers/
│   │   ├── Interfaces/
│   │   ├── Mappers/
│   │   ├── ProgramTests.cs
│   │   └── Services/
│   ├── FrontendConfig.cs
│   ├── insert_test_user.sql
│   ├── Migrations/
│   │   ├── 20250813160516_newmigration.cs
│   │   ├── 20250813160516_newmigration.Designer.cs
│   │   └── AppDbContextModelSnapshot.cs
│   ├── NuGet.Config
│   ├── project.csproj
│   ├── project.http
│   ├── Properties/
│   │   └── launchSettings.json
│   ├── readme.md
│   └── wwwroot/
│       └── uploads/
├── contributors.md
├── frontend/
│   ├── .gitignore
│   ├── .next/
│   ├── eslint.config.mjs
│   ├── next-env.d.ts
│   ├── next.config.js
│   ├── next.config.ts
│   ├── node_modules/
│   ├── package-lock.json
│   ├── package.json
│   ├── postcss.config.mjs
│   ├── public/
│   │   ├── icons/
│   │   └── images/
│   ├── README.md
│   ├── src/
│   │   ├── app/
│   │   │   ├── (auth)/
│   │   │   ├── admin/
│   │   │   ├── client-layout.tsx
│   │   │   ├── dashboard/
│   │   │   │   ├── bookmarks/
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── edit-profile/
│   │   │   │   │   ├── layout.tsx
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── my-events-payments/
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── past-attended-events/
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── past-organized-events/
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── tickets/
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── upcoming-organized-events/
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── upcoming-registered-events/
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── view/
│   │   │   │   │   ├── bookmarked/
│   │   │   │   │   │   └── page.tsx
│   │   │   │   │   ├── created/
│   │   │   │   │   │   └── page.tsx
│   │   │   │   │   ├── past-attended/
│   │   │   │   │   │   └── page.tsx
│   │   │   │   │   ├── past-organised/
│   │   │   │   │   │   └── page.tsx
│   │   │   │   │   ├── registered/
│   │   │   │   │   │   └── page.tsx
│   │   │   ├── event/
│   │   │   │   ├── create-event/
│   │   │   │   │   ├── layout.tsx
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── [id]/
│   │   │   │   │   ├── edit-event/
│   │   │   │   │   │   ├── layout.tsx
│   │   │   │   │   │   └── page.tsx
│   │   │   │   │   ├── page.tsx
│   │   │   │   │   ├── register/
│   │   │   │   │   │   └── page.tsx
│   │   │   │   │   ├── view-event/
│   │   │   │   │   │   └── page.tsx
│   │   │   ├── favicon.ico
│   │   │   ├── globals.css
│   │   │   ├── layout.tsx
│   │   │   ├── page.tsx
│   │   │   ├── payment-cancel/
│   │   │   ├── payment-success/
│   │   │   ├── send-email/
│   │   │   ├── stripe-onboarding-start/
│   │   │   ├── stripe-onboarding-success/
│   │   │   ├── trending-events/
│   │   │   ├── upcoming-events/
│   │   ├── components/
│   │   │   ├── admin-all-payments.tsx
│   │   │   ├── admin-event-income.tsx
│   │   │   ├── admin-payments.tsx
│   │   │   ├── cards/
│   │   │   │   ├── event-card.tsx
│   │   │   │   ├── Navbar.tsx
│   │   │   │   ├── numbers-card.tsx
│   │   │   │   ├── search-bar.tsx
│   │   │   │   ├── swipable-card.tsx
│   │   │   │   └── ticket-card.tsx
│   │   │   ├── common/
│   │   │   │   ├── confirmation-dialog.tsx
│   │   │   │   └── popup-message.tsx
│   │   │   ├── event-form/
│   │   │   │   ├── layout.tsx
│   │   │   │   └── page.tsx
│   │   │   ├── event-list/
│   │   │   │   └── page.jsx
│   │   │   ├── event-live-preview.tsx
│   │   │   ├── footer/
│   │   │   │   └── footer.tsx
│   │   │   ├── profile/
│   │   │   │   ├── change-password-modal.tsx
│   │   │   │   ├── edit-profile-form.tsx
│   │   │   │   ├── profile-details.tsx
│   │   │   │   └── profile-image.tsx
│   │   │   ├── sections/
│   │   │   │   ├── all-events.tsx
│   │   │   │   ├── approved-events.tsx
│   │   │   │   ├── display-event.tsx
│   │   │   │   ├── events-filter.tsx
│   │   │   │   ├── intro-section.tsx
│   │   │   │   ├── trending-events.tsx
│   │   │   │   └── upcoming-events.tsx
│   │   │   └── TermsAndConditions.tsx
│   │   ├── interfaces/
│   │   │   ├── auth.d.ts
│   │   │   ├── nav.d.ts
│   │   │   └── user.d.ts
│   │   ├── middleware.ts
│   │   ├── types/
│   │   │   └── html2canvas.d.ts
│   │   ├── utils/
│   │   │   └── api.ts
│   ├── tailwind.config.js
│   ├── test/
│   │   └── src/
│   │       ├── app/
│   │       └── components/
│   ├── tsconfig.json
├── readme.md
├── start-dev.ps1
```


**API Endpoints**:


<img width="1685" height="917" alt="Screenshot 2025-08-23 105803" src="https://github.com/user-attachments/assets/5270a235-b331-4d99-bf41-1007154036c3" />
<img width="1670" height="914" alt="Screenshot 2025-08-23 105818" src="https://github.com/user-attachments/assets/e6f02e53-c264-4046-860d-613f2c9b0a19" />
<img width="1692" height="917" alt="Screenshot 2025-08-23 110235" src="https://github.com/user-attachments/assets/40118265-9431-4781-8d34-b5429135f5ce" />
<img width="1673" height="917" alt="Screenshot 2025-08-23 110312" src="https://github.com/user-attachments/assets/d9a10f1c-dd19-4d7e-9699-1ccde63de62a" />

**organizer related:** 

Home Page : <img width="1882" height="905" alt="Screenshot 2025-08-22 231752" src="https://github.com/user-attachments/assets/8a512de1-b982-4f85-a3eb-8b8a262870ac" />
Upcoming Events and Filter section: <img width="1896" height="910" alt="Screenshot 2025-08-22 125526" src="https://github.com/user-attachments/assets/52d15c66-b88e-414e-953f-7072b0a80147" />

Trending Events:<img width="1898" height="899" alt="Screenshot 2025-08-23 111746" src="https://github.com/user-attachments/assets/bfbe00e5-6fa2-4222-a947-f587e5cdf31f" />

Footer: <img width="1901" height="915" alt="Screenshot 2025-08-22 125409" src="https://github.com/user-attachments/assets/566ad5aa-13dd-42f6-80a7-ae0972f50f40" />

View Event: <img width="1888" height="914" alt="image" src="https://github.com/user-attachments/assets/d7484047-410d-439b-9885-455c39f546f4" />
<img width="1912" height="909" alt="image" src="https://github.com/user-attachments/assets/4ca6ed42-5c16-44cb-85e8-dfa55462f680" />
<img width="1898" height="908" alt="image" src="https://github.com/user-attachments/assets/01b83bdc-7705-410b-af67-1ac52b4d53b6" />

Create an event and live preview : <img width="1882" height="902" alt="image" src="https://github.com/user-attachments/assets/f7f8bea4-f8ee-46d7-b272-ecf2f2b6e3d4" />
<img width="1900" height="956" alt="image" src="https://github.com/user-attachments/assets/e9427c03-c4d3-4c1d-b228-0b694428ea4e" />

Edit event: <img width="1882" height="902" alt="Screenshot 2025-08-22 132000" src="https://github.com/user-attachments/assets/7fea7de5-6061-4aa8-9bc0-7b768113a52a" />

Bookmarked events: <img width="1901" height="920" alt="Screenshot 2025-08-22 125648" src="https://github.com/user-attachments/assets/7c8eb53d-a735-420f-9676-e2677c3bf503" />

Register : <img width="1866" height="900" alt="Screenshot 2025-08-22 130300" src="https://github.com/user-attachments/assets/a46b7080-0ab8-45f3-b91a-30f1960748eb" />

<img width="1890" height="910" alt="Screenshot 2025-08-22 130319" src="https://github.com/user-attachments/assets/1248960a-f9c3-41ee-8c59-cbbd2f92320d" />

Payment : <img width="1892" height="906" alt="Screenshot 2025-08-22 130702" src="https://github.com/user-attachments/assets/ffd76389-eac0-4c82-9b30-8f44d3db578d" />

Tickets: <img width="1900" height="899" alt="Screenshot 2025-08-22 130748" src="https://github.com/user-attachments/assets/867a8564-3e90-46d8-926b-6bb4cecf70d1" />

Organizer View of Payments: <img width="1900" height="919" alt="image" src="https://github.com/user-attachments/assets/770b4b9c-c849-4f2c-a361-0f97ade70e86" />

Profile : <img width="1906" height="958" alt="image" src="https://github.com/user-attachments/assets/fcd505d9-a67a-4690-a726-249032719716" />

Stripe Connect Page : <img width="1906" height="958" alt="Screenshot 2025-08-22 233529" src="https://github.com/user-attachments/assets/ee2b5cd6-19be-47e1-a271-48ad316138d7" />

Stripe Zero transactions Orders: 

Paid Transactions: 

User reviews: <img width="1893" height="910" alt="Screenshot 2025-08-22 232032" src="https://github.com/user-attachments/assets/b2feafb8-ea0f-4b4d-8e15-019a2cf6b8fe" />


**Admin related:** 

Unapproved Events: <img width="1896" height="898" alt="Screenshot 2025-08-22 130945" src="https://github.com/user-attachments/assets/03c99897-8086-4dd4-9af7-19c4f9803d1e" />

Admin Panel:<img width="1909" height="902" alt="Screenshot 2025-08-22 131030" src="https://github.com/user-attachments/assets/e9cf6325-2e07-4272-9c04-e3ea1f42debb" />

Approved Events: <img width="1896" height="898" alt="Screenshot 2025-08-22 130945" src="https://github.com/user-attachments/assets/4bcd5e88-c214-450b-a358-4976eac21bc9" />

Sending mail to organizer : <img width="1919" height="900" alt="Screenshot 2025-08-22 125202" src="https://github.com/user-attachments/assets/977d9130-e79d-4212-809e-66a55a505ffb" />

Edited Version detection of Admin :<img width="1897" height="913" alt="Screenshot 2025-08-23 111539" src="https://github.com/user-attachments/assets/ef13ce1d-6293-4623-b7ec-40ee80c56d42" />

Admin view of Payments: <img width="1892" height="912" alt="image" src="https://github.com/user-attachments/assets/6e4cef19-6155-4909-a265-bbcdc6a9a8f2" />
<img width="1892" height="916" alt="image" src="https://github.com/user-attachments/assets/aa2086fd-5d74-4ccf-9303-b83f11e97ad7" />
