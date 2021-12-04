# Active Job

Active Job is responsible for creating jobs, i.e. tasks that are performed asynchronously. In addition, it allows them to be queued and run according to the schedule provided. The Active Job module focuses on creating a coherent and logical infrastructure for the job runners no matter what we use.

Like many other things in rails, they have a generator to create them.

```
rails g job do_something
```

The files are located in the **app/jobs** folder and inherit from **ApplicationJob** by default.
They can be assigned to some queue and have only one **perform** method in which we can insert business logic.

``` Ruby
# app/jobs/do_something_job.rb

class DoSomethingJob < ApplicationJob
  queue_as :default

  def perform
    # Do something later
  end
end
```

We can run them using the **perform_later** method, which will do this task in the next free moment.

``` Ruby
DoSomethingJob.perform_later
```

Or at a specific time.

``` Ruby
DoSomethingJob.set(wait_until: Date.tomorrow.noon).perform_later
```

Like controllers, they have callbacks, but they are a bit different:
- before_enqueue
- around_enqueue
- after_enqueue
- before_perform
- around_perform
- after_perform

If we want to queue jobs on production, we have to use some additional library that will allow us to do so. By default, Rails stores jobs in RAM.

The most common example of a job in Rails is sending e-mail. The Action Mailer module is responsible for this.

``` Ruby
SampleMailer.hello(@user).deliver_later
```
