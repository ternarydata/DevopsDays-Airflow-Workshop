# DevopsDays-Airflow-Workshop
Guide for the Airflow Workshop given at SLC DevOps Days 2019.

1. Open the [GCP console](https://console.cloud.google.com). Create an account if necessary. If this is your first time using GCP with this account, you should access to $300 of credit. Otherwise, the costs for working through these examples should be minimal. Just be sure to tear down all resources when you're done.

2. Create a new project. (This will facilitate easy cleanup when we're done.) Name your project something like `airflow-workshop-project`.

3. After a moment, you should get a notice that your project is available. Switch to the new project. (You should see the current project in the blue bar across the top of the page.)

4. In the search box at the top of the screen, type `composer`. Click on the link for the Cloud Composer. Enable the API.

5. Type `composer` in the search box again. Click on the link and you should arrive at the Cloud Composer console. Click _Create_ to create a new environment.

6. For _name_, type `workshop-environment`. For _location_, select `us-central1`. For _Python Version_, select `3`. Click _Create_.

7. You'll arrive back at the Cloud Composer console. Wait for the environment to be available.
