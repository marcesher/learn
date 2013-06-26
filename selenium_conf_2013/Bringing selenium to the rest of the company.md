John Chandler
All Web Leads

Going to talk about how they helped others in All Web Leads get started with selenium

- in 2010, they weren't doing good automated testing
- their first project was to create a live website monitor of their production system, using selenium
- Every 2 minutes, it loaded a different website and worked through normal consumer workflows for the site0 provides screenshots for manual review
- originallly intended to tdetect infrastruccture problems, and worked very well
- woke them up a lot

- after that, they started automating the annoying things they would normally do manually
 - filling out forms, etc
 - automate the slow parts of a manual tests
 - no verification code
- but it wasn't getting them anywhere toward their longer term goals
- then John created an app with WinForms
 - "JayLee"
 - mirrors the forms on their websites
 - they fill out data in jaylee, execute it, and selenium runs and submits that form on the site
  - one thing it can do is fill out a form, but leave the browser up so that you could take it from there

 - continued to improve JayLee, adding new features and also safety checks against hammering production

 - JayLee go to a point where Marketing users started using it
  - this resulted in even further drops in bug numbers

 - then they built stuff into JayLee for use by their sales team
  - sales can then test both dev and live configurations to see what their consumers will see


Where are they now?

 - JayLee is used by about 1/3 of the company across 3 different teams
 - JL is a first-class project supported by the entire engineering team
 - JL helps fill in teh gaps between when a feature goes live and when they write an automated regression test for it
   - only 2 automation devs for a dozen engineers



