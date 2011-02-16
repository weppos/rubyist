# RSpec

## The Rules

RSpec is a great tool in the behavior driven design process of writing
human readable specifications that direct and validate the development
of your application. Follows some guidelines, taken from the literarture
resources and from our experience.

### Describe your methods

Keep clear the methods you are describing using "." as prefix for class
methods and "#" as prefix for instance methods

        # wrong
        describe "the authenticate method for User" do
          ...
        descrive "if the user is an admin" do
          ...

        # correct
        describe '.authenticate' do
          ...
        describe "#admin?"
          ...

### Overuse context and use 'when'/'with' as keys

Contexts are a powerful method to make your tests clear and well organized.
In the long time this way to act will keep tests easy to read

  # wrong
  it "should have 200 stauts code if logged in" do
    it { should respond_with 200 }
    ...
  it "should have 401 stauts code if not logged in" do
    it { should respond_with 401 }


  # correct
  context "when logged in" do
    it { should respond_with 200 }
    ...
  context "when logged out" do
    it { should respond_with 401 }
    ...

### Keep your descriptions short

A spec description should neve be longer than 40 characters. If this
happens, it means you can split it using context (some exceptions are
allowed)

  # wrong
    it "should have 422 status code if an unexpected param wants to be added" do
    ...

  # correct
    context "when not valid"
      it { should respond_with 422 }

As side effect, in the example we removed the description related the
status code, wich has been replaced by the expectation `it { should
respond\_with 422}`. As confirm, if you run this test with the command
`rspec nomefile`, you will obtain an output similar to this.

  when not valid
     it should respond with 422


### Single expectation test

The "one expectation" tip is more broadly expressed as "each test should
make only one assertion. This helps you on finding possible errors,
going directly to the failing test, and to make your code readable.

Note: keep in mind that single expectation test does not
mean single line test.

  # wrong
    it "should create a resource" do
      response.should respond_with_content_type(:json)
      response.should assign_to(:resource
      ...
    end


  # correct
    it { should respond_with_content_type(:json) }
    it { should assign_to(:resource) }
    ...

### Test valid, edge and invalid cases

Testing is a good practice, but if you do not test the edge cases, it
will not be so useful. Lets take as example the following action.

  # extract destroy action
  def destroy
    @resource = Resource.where(:id => params[:id])
    if @resource
      @resource.destroy
      head 204
    else
      render :template => "shared/404", :status => 404,
    end
  end

The error I usually see lie on testing only if the resource has been
removed. But, there is also an edge case, where the resource is not
found, that is important to test. As normal rule think at all the casese
possibilities you can go through, also the strangest ones.

  describe "#destroy" do
    context "when resource is found" do
      it "should render_with 204"
      it "should assigns @resource"
   context "when resource is not found" do
      it "should resnder with 404"
      it "should not assigns @resource"
    end
  end

### Use subject

When you have several tests related to the same "subject" you can use
the `subject{}` method to dry them up.

  # wrong
    it { assigns("message").should match /The resource name is Genoveffa/ }
    it { assigns("message").should match /it has born in Billyville/ }
    it { assigns("message").creator.should match /Claudiano/ }

  # right
    subject { assigns("message") }
    it { should match /The resource name is Genoveffa/ }
    it { should match /it has born in Genopellopoli/ }
    its(:creator) { should match /Claudiano/ }

### Mock or not to mock

Do not (over)use mocks and test real behavior when possible. Anyway, sometimes
they can be really useful, for example if you want to get back a "not found
resource" (one of the few cases I use it)

  # simulate a not found resource
  context "when not found"
    before(:each) do
      Resource.stub(:where).with(:created_from => params[:id]).and_return(false)
      ...
    end
    it { should respond_with 404}
  end

### Create data only when needed

If ever workend in a medium size project (but also in a small ones), test
suites can be heavy to run. To solve this problem, is important to not
load more data than needed. Also if you think you need dozens of record,
usually you are wrong. As dmytro says, add a parameter to the method,
which will limit the number of records to return. In this case you can
create 3 records, and pass 2 as a parameter

  # correct
  describe "User"
    describe ".top" do
      before { (1..3).collect { Factory(:user) }
      it { User.top(2).should have(2).item }
    end
  end

### Use factories and not fixtures

This is an old topic, but it's still good to remember. Do not use
fixture which are difficult to control and use [factories][2]. Use them
to reduce the verbosity on creating new data.

    # wrong
    user = User.create( :name => "Genoveffa",
                        :surname => "Piccolina",
                        :city => "Billyville",
                        :birth => "17 Agoust 1982",
                        :active => true)

    # correct
    user = Factory.create(:user)

When defining a [factory][2], start from a base valid one, which you can easily
extend later on, into the code. If intereste, the [Rails Test prescriptions][12]
book face this problem in deep. It also discuss on why you should not use fixtures
in favour of factories.


### create a do\_action method

While testing rails controllers, I encountered a common pattern on
calling the actions. The code I was gettign through was something like
this.

  # wrong
  post :create, :name   => "Resource Name",
                :scope  => "http://www.example.com/resource/scope",
                :type   => "http://www.example.com/resource/type",
                :format => "json"

The point, is that I was repeating this on several test, so I had to dry
it. The solution was about to create a do\_action method that could
accept some options, so that I could make the same call like this.

  # right
  do\_action(:name => "Another name")

  # do\_action definition
  def do\_action(options = {})
    attributes = { :name   => "Resource Name",
                   :scope  => "http://www.example.com/resource/scope",
                   :type   => "http://www.example.com/resource/type",
                   :format => "json" }
    attributes.merge!(options.symbolize_keys!)
    post :create, attributes
  end

Also if we wrote mode code, we can easily have a default "do\_action"
method which you can use in all of your tests.


## Other (relevant) suggestions

* When something in your application goes wrong, write a test that
  reproduce the error and then correct it. You will gain several hour of
  sleep and more serenity.
* Start writing dirty tests, with long descriptions, without contexts,
  making multiple expectations for test, but then refactor and next time
  follow the right way.
* Use solutions like [autotest][4] to automatically run all of your
  test, withouth thiking about. Combining it with growl, it will become
  one of your best friends.
* Use [TimeCop][5] to mock and test methods that relies on time.
* Use [Webmock][6] to mock HTTP calls to remote service that could not
  be available all the time and that you want to personalize.
* Use a good looking formatter to check if your test passed or failed. I
  use [fuubar][7], which to me looks perfect.


## Literatures

* [The RSpec Book][11]
* [Rails Test Prescriptions][12]
* [Eggs on bread best practices][13]
* [Carbon Five best practices][14]
* [Dmytro best practices][15]
* [Andy Vanasse best practices][16]

  [11]: http://pragprog.com/titles/nrtest/rails-test-prescriptions
  [12]: http://pragprog.com/titles/nrtest/rails-test-prescriptions
  [13]: http://eggsonbread.com/2010/03/28/my-rspec-best-practices-and-tips/
  [14]: http://blog.carbonfive.com/2010/10/21/rspec-best-practices/
  [15]: http://kpumuk.info/ruby-on-rails/my-top-7-rspec-best-practices/
  [16]: http://blog.andyvanasse.com/post/503615383/rspec-best-practices


## LibrariesLibraries

* [RSpec 2][1]
* [Factory girl][2]
* [Shoulda][3]
* [Autotest][4]

  [1]: http://relishapp.com/rspec/rspec-rails
  [2]: http://rdoc.info/github/thoughtbot/factory_girl
  [3]: http://rubydoc.info/github/thoughtbot/shoulda-matchers/master/frames
  [4]: http://ph7spot.com/musings/getting-started-with-autotest
  [5]: https://github.com/jtrupiano/timecop
  [6]: https://github.com/bblimke/webmock
  [7]: http://jeffkreeftmeijer.com/2010/fuubar-the-instafailing-rspec-progress-bar-formatter/


