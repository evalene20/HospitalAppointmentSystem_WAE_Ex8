# Hospital Appointment Booking System

A hospital appointment booking workflow built using **Camunda 8**, **BPMN**, **DMN**, and the **Telegram Bot API**.

The system automatically checks appointment availability, confirms bookings, handles cancellations, and sends Telegram notifications.

## Technologies Used

- Camunda 8.8.32 (C8Run)
- Camunda Desktop Modeler
- BPMN and DMN
- REST Outbound Connector
- Telegram Bot API
- Camunda Operate

## How It Works

1. A patient submits an appointment request.
2. A DMN decision table checks slot availability.
3. If the slot is **AVAILABLE**, the appointment is booked and a confirmation is sent.
4. If the slot is **FULL**, the patient receives a notification.
5. A patient can cancel an active booking, triggering slot release and a cancellation notification.

Telegram notifications are handled by a reusable child process called `send-notification`.

## Project Files

```text
Hospital-Appointment-Booking/
├── booking-process.bpmn
├── send-notification.bpmn
├── slot_decision.dmn
├── Results.pdf
├── README.md
└── Screenshots/
```

## Running the Project

1. Start C8Run.
2. Open the BPMN and DMN files in Camunda Desktop Modeler.
3. Configure `TELEGRAM_BOT_TOKEN` as a runtime secret.
4. Deploy all three files.
5. Start the booking process with sample variables:

```json
{
  "patientId": "P1001",
  "patientName": "Anaya",
  "department": "Cardiology",
  "preferredSlot": "2026-10-30 10:00",
  "bookedCount": 3,
  "telegramChatId": "YOUR_CHAT_ID"
}
```

6. Monitor execution in Camunda Operate at `http://localhost:8080/operate`.

**Note:** Never upload your actual Telegram bot token or `.env` file to GitHub.

## Test Results

| Scenario | Result |
|---|---|
| Successful booking | ✅ Passed |
| Slot full | ✅ Passed |
| Appointment cancellation | ✅ Passed |
| Telegram notifications | ✅ Passed |

All three scenarios were executed successfully.

## Screenshots

Execution screenshots are available in the `Screenshots/` folder, including successful booking, slot-full handling, cancellation, Telegram notifications, and variable propagation.

## Key Concepts Demonstrated

- BPMN workflow automation
- DMN decision tables
- Reusable child processes
- REST API integration
- Message correlation
- Input/output variable propagation
- Workflow monitoring with Camunda Operate

## Conclusion

This project demonstrates an automated hospital appointment booking system using Camunda 8, with decision-based routing, reusable notification processes, and Telegram integration.
