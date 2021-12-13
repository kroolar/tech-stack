# Active Storage

Active Storage allows you to transfer files to cloud storage and allows you to attach these files to Active Record objects

Depending on what we want to store, we have to obtain additional software that will allow us to do so:
- Image (ImageMagick/libvips)
- Video/Audio (ffmpeg)
- PDF (poppler/muPDF)

### Setup

Active Storage uses three tables in the database:

- active_storage_blobs
- active_storage_variant_records
- active_storage_attachments

The following command will start a migration that creates all 3 tables
```
rails active_storage:install
```

The configuration of the services used by the application takes place in the **config/storage.yml** file

``` yml
# config/storage.yml
local:
  service: Disk
  root: <%= Rails.root.join("storage") %>

amazon:
  # attributes for Amazon cloud service
```

Then, in the configuration file, you need to set which website the application should use. It is best to do so separately for each environment.

``` ruby
# config/environment/production.rb
config.active_storage.service = :amazon
```

### Attaching Files
If we want to attach files to our records, we can use the **has_one_attached** and **has_many_attached** methods, which are equivalent to the **has_one** and **has_many** methods for files.

``` Ruby
class User < ApplicationRecord
  has_one_attached :avatar
  has_many :pictures
end
```

### Removing Files

If we want to delete a file we have to use **purge** method instead of **destroy**. The method removes both the record from the database and the file itself from the service that stores it. If we set **ActiveJob**, we can also use the **purge_later** method.

``` Ruby
user.avatar.purge
user.avatar.purge_later
```
### Downloading Files

If we want to download a file, we can do it using the download method or the open method, which downloads the file only temporarily when we want to perform operations on it

``` Ruby
user.avatar.download

user.avatar.open do |file|
  # Change image format
end
```

### Sources:
- https://edgeguides.rubyonrails.org/active_storage_overview.html
