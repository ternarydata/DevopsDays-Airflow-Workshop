# DevopsDays-Airflow-Workshop
Guide for the Airflow Workshop given at SLC DevOps Days 2019.

1. Open the [GCP console](https://console.cloud.google.com). Create an account if necessary. If this is your first time using GCP with this account, you should access to $300 of credit. Otherwise, the costs for working through these examples should be minimal. Just be sure to tear down all resources when you're done.

2. Create a new project. (This will facilitate easy cleanup when we're done.) Name your project something like `airflow-workshop-project`.

3. After a moment, you should get a notice that your project is available. Switch to the new project. (You should see the current project in the blue bar across the top of the page.)

4. In the search box at the top of the screen, type `composer`. Click on the link for the Cloud Composer. Enable the API.

5. Type `composer` in the search box again. Click on the link and you should arrive at the Cloud Composer console. Click _Create_ to create a new environment.

6. For _name_, type `workshop-environment`. For _location_, select `us-central1`. For _Python Version_, select `3`. Click _Create_.

7. You'll arrive back at the Cloud Composer console. Wait for the environment to be available.

8. Clone this git repo.
```
git clone https://github.com/ternarydata/DevopsDays-Airflow-Workshop.git
```

9. In the repo, you'll find three different version of the main DAG file, `workshop-example.py`. These are appeded with 0 through 3 to indicate the different versions.

10. Copy `workshop-example.py.0` to `workshop-example.py`. Click on _DAGs Folder_ in the Cloud Composer console to bring up the GCS bucket containing the Airflow DAGs. Drag and drop `workshop-example.py` into the bucket.

11. Back in the Cloud Composer console, select the Airflow webserver link for the environment. Sign in.

12. You should now see the Airflow DAGs list. You may need to refresh a few times to see `workshop_dag`.

13. If you click on the `workshop_dag` link, you should see the tree view of tasks for two days.

14. Try selecting _Graph View_ to understand DAG dependencies.

15. Next, we'll backfill the DAG to the beginnning of the month. Open the Google Cloud Shell. Make sure you are in the right project. Run the following to backfill to May 1st.
```
gcloud composer environments run --location us-central1 workshop-environment backfill -- workshop_dag -s 2019-05-01 -e 2019-05-14
```

16. Return to the task tree view to watch the tasks kick off and complete. Click the _refresh_ button on the page rather than refreshing the browser will force the web server to refresh and show you the latest data.

17. If you return to Google Cloud Shell and find that the command exited with non-zero status, you may be getting deadlock errors. You'll notice in the tree view that not all tasks have completed. I have not debugged what is causing these errors, but you can run the backfill command again. It will eventually complete successfully.

18. Next, we'll add a new task with no dependencies. Copy `workshop-example.py.1` to `workshop-example.py` and upload. (You will need to resolve an upload conflict by selecting _replace_.)

19. You will eventually see `new_task` in the web interface. You can see in _Graph View_ that the task has no dependencies.

20. Next, add the dependency edges for `new_task` by copying and uploading `workshop-example.py.2`.

21. Backfill again in the Cloud Shell to run the new tasks.

22. Next, we'll remove `run_this_last`, both in the database and the DAG definition file.
To remove it in the DAG definition file, go to the _Tree View_. Click on one of the boxes (task instances) for this task. Select _task instances_. Select all and delete. Return to the tree view to see that the instances for this task have been cleared, but instances for other tasks remain.

23. We update the DAG definition file to remove all mentions of `run_this_last`. Copy and upload `workshop-example.py.3`.

24. Next, we'll add a BigQuery task. Copy and upload `workshop-example.py.4`. Look at the code. Backfill to run the task instances.

25. When you are done, tear everything down to make sure you don't incur additional GCP charges. The easiest option is to delete `airflow-workshop-project`. To do this, click on the project name in the bar at the top of the screen. Click on the three dot menu in the upper right hand corner of the pop up box. Click _manage resources_. Check the box next to `airflow-workshop-project`. Follow the instructions to delete the project.

26. Verify that your project has been deleted so you don't accidentally incur extra charges.
