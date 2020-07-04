# OpenSSL::SignatureAlgorithm

Provides `OpenSSL::SignatureAlgorithm::ECDSA`, `OpenSSL::SignatureAlgorithm::RSAPSS`
and `OpenSSL::SignatureAlgorithm::RSAPKCS1` ruby object wrappers on top of `OpenSSL::PKey::EC`
and `OpenSSL::PKey::RSA`, so that you can reason in terms of signature algorithms when
signing and/or verifying signatures, instead of keys.

[![Gem](https://img.shields.io/gem/v/openssl-signature_algorithm.svg?style=flat-square&color=informational)](https://rubygems.org/gems/openssl-signature_algorithm)
[![Travis](https://img.shields.io/travis/cedarcode/openssl-signature_algorithm/master.svg?style=flat-square)](https://travis-ci.org/cedarcode/openssl-signature_algorithm)

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'openssl-signature_algorithm'
```

And then execute:

    $ bundle install

Or install it yourself as:

    $ gem install openssl-signature_algorithm

## Usage

### ECDSA

```ruby
to_be_signed = "to-be-signed"

# Signer
algorithm = OpenSSL::SignatureAlgorithm::ECDSA.new
signing_key = algorithm.generate_signing_key
signature = algorithm.sign(to_be_signed)

# Signer sends verify key to Verifier
verify_key_string = signing_key.verify_key.serialize

# Verifier
verify_key = OpenSSL::SignatureAlgorithm::ECDSA::VerifyKey.deserialize(verify_key_string)
algorithm = OpenSSL::SignatureAlgorithm::ECDSA.new
algorithm.verify_key = verify_key
algorithm.verify(signature, to_be_signed)
```

### RSA-PSS

```ruby
to_be_signed = "to-be-signed"

# Signer
algorithm = OpenSSL::SignatureAlgorithm::RSAPSS.new
signing_key = algorithm.generate_signing_key
signature = algorithm.sign(to_be_signed)

# Signer sends verify key to Verifier
verify_key_string = signing_key.verify_key.serialize

# Verifier
verify_key = OpenSSL::SignatureAlgorithm::RSAPSS::VerifyKey.deserialize(verify_key_string)
algorithm = OpenSSL::SignatureAlgorithm::RSAPSS.new
algorithm.verify_key = verify_key
algorithm.verify(signature, to_be_signed)
```

### RSA-PKCS1_v1.5

```ruby
to_be_signed = "to-be-signed"

# Signer
algorithm = OpenSSL::SignatureAlgorithm::RSAPKCS1.new
signing_key = algorithm.generate_signing_key
signature = algorithm.sign(to_be_signed)

# Signer sends verify key to Verifier
verify_key_string = signing_key.verify_key.serialize

# Verifier
verify_key = OpenSSL::SignatureAlgorithm::RSAPKCS1::VerifyKey.deserialize(verify_key_string)
algorithm = OpenSSL::SignatureAlgorithm::RSAPKCS1.new
algorithm.verify_key = verify_key
algorithm.verify(signature, to_be_signed)
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/cedarcode/openssl-signature_algorithm.
