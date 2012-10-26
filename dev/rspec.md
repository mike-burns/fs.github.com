---
layout: default

---

# RSpec Best Practices.

You should cover validations, associations with shoulda matchers and test deeply
complected model methods.
Check out for example user_spec.rb

    describe User do
      it { should allow_mass_assignment_of(:full_name) }
      it { should allow_mass_assignment_of(:email) }
      it { should allow_mass_assignment_of(:password) }
      it { should allow_mass_assignment_of(:password_confirmation) }

      it { should validate_presence_of :full_name }
    end


Use shortcuts `let`, `it {}` and `subject {}`

    subject { @user.address }
    it { should be_valid }


Start context with ‘when’/'with’ and methods description with ‘#’

Use RSpec matchers to get meaningful messages

    it { should be_valid }


Only one expectation per it block

    describe DemoMan do
      let(:demo_man) { DemoMan.new }
      subject { demo_man }

      it { should respond_to :name   }
      it { should respond_to :gender }
      it { should respond_to :age    }
    end


(Over)use describe and context

    describe User do
      let(:user) { User.new }
      subject { user }

      context "when name empty" do
        it { should not be_valid }
        it { save.should be false }
      end

      context "when name not empty" do
        before { user.name = 'Sam' }

        it { should be_valid }
        it { save.should be true }
      end

      describe :present do
        subject { user.present }

        context "when user is a W" do
          before { user.gender = 'W' }

          it { should be_a Flower }
        end

        context "when user is a M" do
          before { user.gender = 'M' }

          it { should be_an IMac }
        end
      end
    end


Test Valid, Edge and Invalid cases

    describe "#month_in_english(month_id)" do
      context "when valid" do
        it "should return 'January' for 1" # lower boundary
        it "should return 'March' for 3"
        it "should return 'December' for 12" # upper boundary
      context "when invalid" do
        it "should return nil for 0"
        it "should return nil for 13"
      end
    end

http://eggsonbread.com/2010/03/28/my-rspec-best-practices-and-tips/
http://betterspecs.org/
