# Approach
- provide a bridge from your understanding of Ruby and Rails to the Elixir and Phoenix world as a foundation for learning further
- this is not a detailed instructional course into the platform
- rather focused on reducing the growing pains of moving to the platform
- provide a guided-tour of the platform and eco-system
- "on-demand" learning, demonstrate then explain the concepts and tools
- produce a basic CRUD Phoenix app by the end of session
- welcome question along the way
- no need to follow along, record the session for review at a later time

# Sessions
1. Introduction to Conventional Programming in Elixir, Basic Ecto and Phoenix (Nov 1)
2. Introduction to Concurrent Programming and more Ecto (to be scheduled)

# Agenda for first session (with two breaks after 50mins for 10mins)
- Building your first Elixir Application
- Introduction to Ecto
- "Out-of-the-box" Phoenix Walkthrough
- Generated "resource" walkthrough

# About the demo application
- restaurant reservation application
- making a reservation for a number of people, for a given day
- data model: Reservation{date, name, email, quantity}, Comment{body}
- Part one (today): build an admin interface for managing reservations
- Part two (next time): build a public interface validating reservations based on restaurant capacity

# 1. Getting started
- assume Elixir installed
	- [home brew](http://elixir-lang.org/install.html#mac-os-x)
	- [ASDF](https://github.com/asdf-vm/asdf)
	- note: Elixir has a dependency on Erlang
	- [Erlang History](https://github.com/ferd/erlang-history)
	- Dash
- three major components to Erlang
	- Erlang Language
	- OTP (Open Telecom Platform), a collection of middleware, libraries tools
		- e.g. GenServer this library provides these behaviours
	- BEAM (Bogdan/Bjorn's Erlang Abstract Machine)
		- aka Erlang VM
		- think JVM
- Elixir is compiled to byte code (i.e. BEAM files) that run on the VM
- Elixir and Erlang are interoperable

# 2. Getting your feet wet
- starting REPL
- iex == irb
- demonstrate strings
- `String.upcase("foo bar")`
- think in data transformations
- pipeline example:  `String.upcase("foo bar") |> String.split(" ") |> Enum.map(fn(e) -> e <> "-hello" end)`
- exit the IEx

# 3. Generating your first Elixir application
- `mix new rezzy`
- `mix test`
- BEAM files are compiled under `_build`
- first time install the package manager "Hex"
	- `mix local.hex`
	- mix == rake + bundler
		- `mix help`
	- hex == RubyGems
	- hex.pm == rubygems.org
- [Elixir Forum](https://elixirforum.com/)
- `test.watch` package
- `mix deps.get`
- `mix help` # => show the package help listed
- dependencies are stored in `./deps` so no need for "gemsets"
-  demo `mix test.watch`
- `cat mix.lock`

## Write the first test
- generate a basic application for adding reservations
- exploring key elixir concepts
	- pattern matching
	- understanding non-scalar data-types
	- sigils
	- working with DateTime types
	- pipelines

## Implement with an In-Memory Repo
- uses a struct for Reservation
- uses a simple GenServer (Agent)

# 4. Introducing Ecto
- replace the in-memory Repo with Ecto
- Ecto changesets
- [validations](https://hexdocs.pm/ecto/Ecto.Changeset.html)
- [learning more](https://github.com/civilcode/playbook/blob/master/education/trails/elixir/ecto.md)

# 5. Generating your first Phoenix application
- install Phoenix generator to create a new application
	- `mix archive.install https://github.com/phoenixframework/archives/raw/master/phoenix_new.ez`
	- archive is a Zip file which contains an application as well as its compiled BEAM files
	- the archive will be available globally
- generate the a new application
	- `mix phoenix.new rezzy_admin`
	- caveat: generators are a great learning tool
	- directory walkthrough

## Asset Pipeline
- npm / brunch
- `cat package.json`
- `cat brunch-config.js`
- web/static vs priv/static

## Phoenix Walkthrough
- "App" module
- Endpoint
- Router
- Controller
- View
- Template
- `Phoenix.View.render(RezzyWeb.PageView, "index.html", [])`

# 6. Generating a Resource
- `mix phoenix.gen.html Reservation reservations reserved_for:date name email quantity:integer`
- ignore instructions `mix ecto.migrate`
- explain the application is being compiled, missing route function
- follow instructions, adding route, then migrate
- add scoping
- demonstrate routes `mix phoenix.routes`
- walk-through the generated resource
- explain the relation between changesets and forms
- model -> schema
- add a unique constraint to Reservations

# 7. Review Architecture
- umbrella apps
- separate the domain from the "web" interface
