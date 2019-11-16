# S3 Uploads in Custom with Active Storage

## Setup
Add to gemfile
```ruby 
gem "aws-sdk-s3"
gem "mini_magick"
gem "activestorage"
gem "activestorage-validator"
```

## Add Storage.yml
```ruby
# config/storage.yml
test:
  service: Disk
  root: <%= Rails.root.join("tmp/storage") %>

local:
  service: Disk
  root: <%= Rails.root.join("storage") %>

amazon:
  service: S3
  access_key_id: <%= ENV['AWS_ACCESS_KEY_ID'] %>
  secret_access_key: <%= ENV['AWS_SECRET_ACCESS_KEY'] %>
  region: <%= ENV["AWS_S3_REGION"] %>
  bucket: <%= ENV['AWS_S3_BUCKET'] %>
  endpoint: <%= ENV["AWS_S3_ENDPOINT"] %>
  force_path_style: true
```

## Model
```ruby 
class Upload < ApplicationRecord
  has_one_attached :file_upload
  validates :file_upload, blob: { content_type: ['image/png', 'image/jpg', 'image/jpeg'], size_range: 1..100.megabytes }

  has_many_attached :file_collection

  def thumb
    if self.file_upload.attachments && self.file_upload.attachments.count > 0
      if self.file_upload.attachments.first.content_type == "image/svg+xml"
        self.file_upload.attachments.first.service_url
      else
        self.file_upload.attachments.first.variant(combine_options: { resize: '200>', gravity: 'Center', crop: '200x200+0+0' }).processed.service_url
      end
    else
      self.default_image
    end
  end

  def preview_thumb
    if self.file_upload.attachments && self.file_upload.attachments.count > 0
      self.file_upload.attachments.first.preview(resize: "400x400").processed.service_url
    else
      self.default_image
    end
  end

  def medium
    if self.file_upload.attachments && self.file_upload.attachments.count > 0
      if self.file_upload.attachments.first.content_type == "image/svg+xml"
        self.file_upload.attachments.first.service_url
      else
        self.file_upload.attachments.first.variant(combine_options: { resize: '500>', gravity: 'Center', crop: '500x500+0+0' }).processed.service_url
      end
    else
      self.default_image
    end
  end

  def large
    if self.file_upload.attachments && self.file_upload.attachments.count > 0
      if self.file_upload.attachments.first.content_type == "image/svg+xml"
        self.file_upload.attachments.first.service_url
      else
        self.file_upload.attachments.first.variant(combine_options: { resize: '1100>', gravity: 'Center', crop: '1100x1100+0+0' }).processed.service_url
      end
    else
      self.default_image
    end
  end

  def original
    if self.file_upload.attachments && self.file_upload.attachments.count > 0
      self.file_upload.attachments.first.service_url
    else
      self.default_image
    end
  end

  def default_image
    "https://images.unsplash.com/photo-1554051852-b6639645165b?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=934&q=80"
  end

  def is_image?
    self.content_type =~ %r(image) && self.file_upload.first.content_type != 'image/svg+xml'
  end

  def is_svg?
    self.content_type == 'image/svg+xml'
  end

  def is_video?
    self.content_type =~ %r(video)
  end

  def is_audio?
    self.content_type =~ /\Aaudio\/.*\Z/
  end
end
```
