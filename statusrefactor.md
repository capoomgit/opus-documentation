# Job Status Update

In order to streamline our pipeline and reduce overhead, we have updated the job status indications within OPUS.

## Previous Job Statuses
Our old statuses were as follows:
- `PENDING`: The job was in queue, waiting to be processed.
- `IN_PROGRESS`: The job was currently being processed.
- `COMPLETED`: The job finished successfully.
- `FAILED`: The job encountered an error and could not complete.
- `CANCELLED`: The job was cancelled by the user or system.

## Updated Job Statuses
Our new statuses provide more detail and are now as follows:
- `Queued`: The job is in the queue, waiting for assignment.
- `Pending`: The job is waiting for its dependencies to be satisfied.
- `Running`: The job is currently in progress.
- `Completed`: The job has successfully finished.
- `Suspended`: The job is on hold or temporarily stopped.
- `Failed`: The job encountered an error and could not complete.

We believe this change will provide more precise information on job status and aid in optimizing our workflow.