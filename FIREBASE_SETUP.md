# Bayariq Daily Report — Firebase collaboration (development only)

Production GitHub Pages URL stays unchanged. Do not merge this branch until authentication, Firestore rules and simultaneous editing are tested.

Firebase project ID: bayariq-daily-report
Web app auth domain: bayariq-daily-report.firebaseapp.com

## Account model
Users see username + password. Internally Firebase Email/Password requires a synthetic email per account (e.g. admin@bayariq-login.invalid); these addresses are not real mailboxes and cannot receive password-reset emails. Create accounts only via Firebase Console or trusted Admin SDK, never with public sign-up. Do not store passwords in Firestore or GitHub.

profiles/{uid}: {role: "admin" | "primary" | "intermediate" | "secondary" | "special", username: "..."}
Provision profiles manually from Firebase Console initially. Firestore rules deny clients changing roles.

## Before publishing
1. Create five Auth accounts with strong unique passwords, record their UIDs.
2. Create matching profiles in Firestore using those UIDs.
3. Review and deploy firestore.rules (do not use test mode).
4. Integrate SDK in index.html on this branch, mapping each editable table cell to an immutable section; sync individual cells and keep global date/admin fields admin-only.
5. Add the deployed GitHub Pages domain to Firebase Auth authorized domains.
6. Test anonymous denial, cross-section write denial, manager access, two simultaneous users, conflict behavior, printing and existing formatting.
7. Only then merge into main; GitHub Pages URL remains the same.

Status: Rules draft only; frontend not yet connected; no live changes.
