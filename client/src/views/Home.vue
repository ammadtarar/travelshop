<template>
  <div class="home">
    <header class="top-bar">
      <div class="inner">
        <img src="../assets/logo.png" alt="" />
      </div>
    </header>
    <div class="content">
      <div class="top-info-container">
        <div class="img-book-container">
          <ImagesSlide :images="images" />
        </div>
        <div class="details-container">
          <span class="green-tag">Book With Flexibility</span>
          <span class="title">8 Day Sail Croatia Split Blue Cruise Tour</span>
          <div class="days-rating-cont">
            8 Days • 4.8
            <img src="../assets/ic_star.png" alt="rating" />
            <span class="count">(239)</span>
          </div>

          <span class="start-end-cont"> Start and end in <b>Split</b> </span>

          <div class="tags">
            <span class="tag" v-for="tag in tags" v-bind:key="tag">{{
              tag
            }}</span>
          </div>

          <div class="kv-container">
            <div class="kv" v-for="info in infos" v-bind:key="info.key">
              <span class="key">{{ info.key }}</span>
              <span class="val">{{ info.val }}</span>
            </div>
          </div>

          <div class="card">
            <div class="discount-container">
              From
              <del>$1,350</del>
              <span class="percent">-45%</span>
            </div>
            <div class="price-container">
              <span class="currency">US</span>
              <span class="amount">$743</span>
            </div>
            <div class="actions-container">
              <button class="check">Check Availability</button>
              <img src="../assets/ic_not_fav.png" alt="" class="fav" />
            </div>

            <div class="extra">
              <img src="../assets/pay_more.svg" alt="" />
              <span>
                <b>Pay over time</b>
                with smaller, interest free installments
              </span>
            </div>

            <div class="extra">
              <img src="../assets/book_once.svg" alt="" />
              <span>
                <b>Book once</b>
                and share the cost with split payments
              </span>
            </div>
          </div>
        </div>
      </div>

      <div class="places-container">
        <div class="planning-container">
          Start planning your tour
          <IconButton title="Download Brochure" icon="ic_download.svg" />
          <IconButton title="Ask a Question" icon="ic_ask.svg" />
        </div>

        <span class="heading">Places You'll See</span>
        <PlacesGallery :places="places" name="places" />
        <MapView />

        <span class="heading">Highlights</span>
        <div class="highlights">
          <div
            class="highlight"
            v-for="highlight in highlights"
            v-bind:key="highlight"
          >
            <img src="../assets/ic_tick.svg" />
            {{ highlight }}
          </div>
        </div>

        <span class="heading">Ready-to-book adventures, personalized</span>

        <div class="features">
          <div class="feature" v-for="feature in features" v-bind:key="feature">
            <img
              :src="require(`../assets/${feature.icon}`)"
              :alt="feature.title"
            />
            <div class="info">
              <span class="title">{{ feature.title }}</span>
              <span class="desc">{{ feature.desc }}</span>
            </div>
          </div>
        </div>

        <span class="heading">Itinerary</span>
        <span class="overview">{{ overview }}</span>

        <Itinerary :data="Itinerary" />

        <div class="download-brochure">
          <img src="../assets/ic_brochure.svg" />
          <div class="info">
            <span class="title">Want to read it later?</span>
            <span class="desc"
              >Download this tour’s PDF brochure and start tour planning
              offline</span
            >
          </div>
          <button class="hollow-btn">Download Brochure</button>
        </div>

        <div class="policy-container">
          <span class="banner">Book With Flexibility</span>
          <span class="title">Your Peace of Mind Options</span>
          <div class="policies">
            <div
              class="policy"
              v-for="policy in policies"
              v-bind:key="policy.title"
            >
              <img
                :src="require(`../assets/${policy.icon}`)"
                :alt="policy.title"
              />
              <span class="title">{{ policy.title }}</span>
              <span class="desc">{{ policy.desc }}</span>
            </div>
          </div>

          <button class="hollow-btn">Explore your options</button>
        </div>

        <span class="heading">What's Included</span>
        <IncludedExcludedView :data="included" />

        <span class="heading">Where You'll Stay</span>

        <div class="stays">
          <div class="stay">
            <img src="../assets/ic_stay.svg" alt="stay" />
            Hotel
          </div>
          <div class="stay">
            <img src="../assets/ic_stay.svg" alt="stay" />
            Cruise Ship
          </div>
        </div>

        <span class="heading">Customer Photos</span>
        <PlacesGallery
          :places="customerPhotos"
          name="cutomerPhotos"
          style="margin-top: -0.5rem; margin-bottom: 4rem"
        />

        <span class="heading">Customer Reviews</span>
        <ServiceRatings :ratings="customerRatings" />
        <Reviews :reviews="reviews" />

        <span class="heading">Dates & Availability</span>
        <div class="credit-cards">
          No Credit Card Fees
          <img
            src="https://cdn.tourradar.com/images/responsive/payment_providers/card_logos/PayPal.png"
          />
          <img
            src="https://cdn.tourradar.com/images/responsive/payment_providers/card_logos/American-Express.png"
          />
          <img
            src="https://cdn.tourradar.com/images/responsive/payment_providers/card_logos/Maestro.png"
          />
          <img
            src="https://cdn.tourradar.com/images/responsive/payment_providers/card_logos/MasterCard.png"
          />
          <img
            src="https://cdn.tourradar.com/images/responsive/payment_providers/card_logos/Visa.png"
          />
        </div>

        <div class="availability-container">
          <span class="days">8 Days</span>
          <span class="title">8 Day Sail Croatia Split Blue Cruise Tour</span>
          <soab class="dest">Start and ends in Split</soab>
          <div class="tour-actions">
            <div
              class="action"
              :class="{ selected: availabilityType === 'group' }"
              @click="availabilityType = 'group'"
            >
              <img src="../assets/ic_group.svg" />
              Group Tour
            </div>
          </div>

          <div class="group-availability">
            <div class="cards">
              <div class="card">
                <img src="../assets/ic_flex.svg" />
                <span class="title">Book With Flexibility</span>
                <p class="desc">
                  You're not locked in! Make changes to your dates or switch
                  tours.
                </p>
              </div>
              <div class="card">
                <img src="../assets/ic_installments.svg" />
                <span class="title">Pay-by-instalments</span>
                <p class="desc">
                  Take advantage of our 0% interest instalment plan on selected
                  departures.
                </p>
              </div>
            </div>

            <span class="sub-heading">Select a departure month</span>
            <div class="dates-container">
              <button
                :class="{ selected: dateIndex == 0 }"
                @click="dateIndex = 0"
              >
                Upcoming Departures
              </button>
              <button
                :class="{ selected: dateIndex == 1 }"
                @click="dateIndex = 1"
              >
                October 2021
              </button>
              <button
                :class="{ selected: dateIndex == 2 }"
                @click="dateIndex = 2"
              >
                November 2021
              </button>
              <button
                :class="{ selected: dateIndex == 3 }"
                @click="dateIndex = 3"
              >
                December 2021
              </button>
            </div>

            <span class="sub-heading">Available Departues</span>

            <div class="departures">
              <div
                class="departure"
                v-for="(item, index) in departures"
                v-bind:key="index"
              >
                <div class="top">
                  <div class="dates">
                    <span class="day">{{ item.start.day }}</span>
                    <span class="date">{{ item.start.date }}</span>
                  </div>
                  <img src="../assets/ic_arrow_right.svg" class="arrow" />
                  <div class="dates">
                    <span class="day">{{ item.end.day }}</span>
                    <span class="date">{{ item.end.date }}</span>
                  </div>

                  <div class="prices">
                    <span class="old"
                      ><del>{{ item.prices.old }}</del></span
                    >
                    <span class="new">{{ item.prices.new }}</span>
                  </div>

                  <div class="prices lang-container">
                    <span class="old">Language</span>
                    <span class="new">{{ item.language }}</span>
                  </div>
                </div>
                <button class="confirm">Confirm Date</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import ImagesSlide from "@/components/ImagesSlide.vue";
import IconButton from "@/components/IconButton.vue";
import PlacesGallery from "@/components/PlacesGallery.vue";
import MapView from "@/components/MapView.vue";
import Itinerary from "@/components/Itinerary.vue";
import IncludedExcludedView from "@/components/IncludedExcludedView.vue";
import ServiceRatings from "@/components/ServiceRatings.vue";
import Reviews from "@/components/Reviews.vue";

export default {
  name: "Home",
  components: {
    ImagesSlide,
    IconButton,
    PlacesGallery,
    MapView,
    Itinerary,
    IncludedExcludedView,
    ServiceRatings,
    Reviews,
  },
  data() {
    return {
      dateIndex: 0,
      availabilityType: "group",
      images: [
        "img_1.jpeg",
        "img_2.jpeg",
        "img_3.jpeg",
        "img_4.jpeg",
        "img_5.jpeg",
        "img_6.jpeg",
        "img_7.jpeg",
        "img_8.jpeg",
        "img_9.jpeg",
        "img_10.jpeg",
      ],
      tags: [
        "Adventure",
        "Cruise",
        "Group Travel",
        "28 Guests",
        "Easy",
        "Fully Guided",
        "Budget Class",
        "Comfort",
        "Best Prices Gurantee",
        "Customer Case 24/7",
      ],
      infos: [
        { key: "Tour Operator", val: "Travel Shop" },
        { key: "Max Group Size", val: "28" },
        { key: "Age Range", val: "18 to 85" },
        { key: "Operated In", val: "English" },
        { key: "Tour ID", val: "91447" },
      ],
      places: [
        { img: "img_9.jpeg", name: "Split" },
        { img: "img_8.jpeg", name: "Makarska" },
        { img: "img_7.jpeg", name: "Mijet" },
        { img: "img_6.jpeg", name: "Dubrovnik" },
        { img: "img_5.jpeg", name: "Korcula" },
        { img: "img_4.jpeg", name: "Hvar" },
      ],
      highlights: [
        "Fall in love with the sights, sounds and tastes of India",
        "Live like royalty while staying at the Sardargarh Fort",
        "See cheetahs, panthers and tigers on an incredible safari",
        "Visit the Amber Fort in Jaipur and the palace in Udaipur",
        "Take a picture in front of the ivory Taj Mahal",
      ],
      features: [
        {
          icon: "ic_personal.svg",
          title: "Personal",
          desc: "Make your adventure more you",
        },
        {
          icon: "ic_private.svg",
          title: "Private",
          desc: "Enjoy a tour focused solely on your travel group",
        },
        {
          icon: "ic_professional.svg",
          title: "Professional",
          desc: "Access our Travel Experts’ insider knowledge",
        },
        {
          icon: "ic_protected.svg",
          title: "Protected",
          desc: "Travel within your own bubble",
        },
      ],
      overview:
        "A sail Croatia cruise starting from the inspiring city of Split. Journeying along the beautiful Adriatic water stopping at the unforgettable islands of Mljet, Korcula and Hvar, whilst also stopping at different island bays and beaches for swimming and relaxation. Among the beautiful islands, the Croatia cruise will take you to the city of Makarska and its astounding surrounding mountains. The opposite end of the cruise is the city of Dubrovnik. After exploring this inspirational town and seeing some of the sets for Game of Thrones it is time to return to the city of Split, visiting different islands from the first part of the journey. Our Turkey-Croatia boat charters and cabin cruises are a great way to discover Croatia by yacht, you will experience wonderful natural scenery and unique historical & archaeological monuments. ",
      Itinerary: [
        {
          isExpanded: false,
          title: "Day 1 : Split - Makarska",
          desc: "On the first day, the captain and crew will be waiting to greet everyone on the sail Croatia cruise. 1 pm is the departure time, allowing for swimming while everyone gets to know each other. Arrival to Makarska in the late afternoon allows for time to explore the town and find a suitable restaurant amongst those available. Once the sun goes down there is a famous ‘club in a cave’ that should be visited, going by the name Club Deep.",
        },
        {
          isExpanded: false,
          title: "Day 2: Makarska – Mljet",
          desc: "Todays Croatia cruise starts early to heading to Mljet Island. As the captain sails to one of the villages, Pomena or Polace, on the island that is dominated by a national park. The national park is a contrast to the nightlife that is offered in other places on this cruise. The nature park that this island is dominated has a few was to be explored. Some like to hire a bicycle as follow the set routes that show some amazing views. An alternative option is to paddle on the lake by hiring a kayak",
        },
        {
          isExpanded: false,
          title: "Day 3: Mljet – Dubrovnik",
          desc: "Around the island of Mljet are beautiful bays that the captain will take you to on today's sail Croatia journey. Once swimming has been finished the next route takes you past the Elphaite archipelago, an unforgettable sight.Your Croatia cruise arrives in Dubrovnik in the early afternoon, allowing for free time to explore and visit some of the cliff-side bars, which are in the ideal place to watch the sunset over the blue Adriatic S",
        },
        {
          isExpanded: false,
          title: "Day 4: Dubrovnik",
          desc: "Today you will take a break from Sail Croatia as there is more to see and do in this unusual city. For those who are film and tv fans, why not visit the setting for Kings Landing, Capital of Westeros From the popular tv adaptation of The Game of Throne book. Outside the city holds as many amazing views as inside does. Try heading to the top of Mount Srd either by taking the relaxing cable car or the exciting off-road buggy tour.",
        },
        {
          isExpanded: false,
          title: "Day 5: Dubrovnik – Korcula",
          desc: "Continuing on your Sail Croatia tour the heading to the island of Korcula, the town that shares the islands name is today’s final dock of the day.The old city is a mixture of buildings from various periods throughout history. Throughout the town, there are small bars that have street parties late into the night.",
        },
        {
          isExpanded: false,
          title: "Day 6: Korcula – Hvar",
          desc: "From Korcula, you will head to Hvar island aiming for the small harbour at its main town. Due to restrictions upon arrival, lunch will be served on the boat as normally the Croatia cruise docks in the late afternoon. Once on the island, the nightlife will capture everyone’s attention, starting with watching the sunset at the popular Hula Hula bar before heading to the famous ‘club on an island’ Carpe Diem.",
        },
        {
          isExpanded: false,
          title: "Day 7: Hvar – Split",
          desc: "On the final full day on the sail Croatia cruise the captain will stop at one of the Pakleni Islands near Hvar, once everyone is back onboard the captain will continue the journey to the city of Split by heading past the famous Bol’s Zlatni Rat, commonly known as Golden Horn.You will dock in the city of Split in the afternoon, allowing free time to explore this bustling metropolis with its unmissable sights. One that is recommended to visit is the Diocletian’s Palace, a walled area of the city that was once a working palace.",
        },
        {
          isExpanded: false,
          title: "Day 8: Split",
          desc: "After breakfast it is time to make final goodbyes, although check-out is at 9 am this does not mean that your exploration of this amazing country stops. So why not take another tour or visit one of the many landmarks in Split that asma",
        },
      ],
      policies: [
        {
          icon: "ic_credit.svg",
          title: "Credit for Future Tours",
          desc: "Convert your booking to credit for future bookings.",
        },
        {
          icon: "ic_dates.svg",
          title: "Date Changes",
          desc: "This operator allows date changes after booking",
        },
        {
          icon: "ic_cancel.svg",
          title: "Cancellation Policy",
          desc: "A transparent overview of applicable fees.",
        },
      ],
      included: [
        {
          isExpanding: false,
          included: true,
          title: "Accommodation",
          desc: "Two vessel options are available. Flagship ‘Novi Dan’ and the sister ship ‘Mihovil’.-Novi Dan – Air-Conditioning in cabins. Ensuite shower rooms and toilets as standard. Free wi-fi on board.-Otac Duje - Air-Conditioning in the cabins. Ensuite bathroom including; shower, sink, and toilet as standard. Free Wi-Fi onboard.",
        },
        {
          isExpanding: false,
          included: true,
          title: "Meals",
          desc: "Half board accommodation including breakfast and lunch unless stated otherwise in your itinerary.Unlimited drinking water per person per day. On this cruise, you may not bring along your own drinks. A bar tab is set up for the duration of the Cruise. All bar tabs are paid on the conclusion of your cruise. For any dietary requirements, please inform us prior to travel, onboard cooks will try to accommodate.",
        },
        {
          isExpanding: false,
          included: true,
          title: "Transport",
          desc: "Traditional, Croatia-built wooden cruise vessels. Modern cabins and facilities with a vintage style. Novi Dan’s 15 cabin capacity offers a person capacity of 30 to 38 passengers. Otac Duje is the sister ship offering 13 ensuite cabins with overnight air-conditioning available, with a capacity of 26 to 28 passengers.",
        },
        { isExpanding: false, included: true, title: "Optional", desc: "" },
        {
          isExpanding: false,
          included: true,
          title: "Other included",
          desc: "Please check the information below before your departure : 1- International & Domestic Flight Tickets. 2- Covid-19 PCR Test. 3- Tour Itinenary. 4- Confirmed Documents are sent by us to include Hotel reservations etc. 5- Domestic Flight Tickets if any (Please check your title/name spelling printed correctly). 6- Passport Validation Terms. 7- Visa if needed (check before your trip for the dates on your visa). 8- If visa needed, please ask us for invitation letter to ease the visa application process. 9- Flight details for on time Airport transfer services. 10- Observe the luggage limitation by Airlines for domestic flights if any. 11- Obtain emergency contact details from our office",
        },
        {
          isExpanding: false,
          included: false,
          title: "Hygiene protocol",
          desc: "-Port and marina fees, taxes and fuel are all included in your cabin charter package price.-Captain and Crew -Linen is provided on this cabin charter. Please note that you must bring along your own bath/beach towel. No towels are provided. -Onboard tour leader -Unlimited drinking water per day per person -Free Wi-fi",
        },
        {
          isExpanding: false,
          included: false,
          title: "Flights",
          desc: "• International and Domestic Flights",
        },
        {
          isExpanding: false,
          included: false,
          title: "Insurance",
          desc: "• Insurance: All types",
        },
      ],
      customerPhotos: [
        { img: "img_9.jpeg", name: "" },
        { img: "img_8.jpeg", name: "" },
        { img: "img_7.jpeg", name: "" },
        { img: "img_6.jpeg", name: "" },
        { img: "img_5.jpeg", name: "" },
        { img: "img_4.jpeg", name: "" },
      ],
      customerRatings: {
        overall: { rating: "Excellent", score: "4.8" },
        others: [
          {
            name: "Itinerary",
            rating: "Excellent",
            score: "4.9",
            icon: "ic_itinerary.svg",
          },
          {
            name: "Guide",
            rating: "Excellent",
            score: "4.8",
            icon: "ic_guide.svg",
          },
          {
            name: "Transport",
            rating: "Excellent",
            score: "4.9",
            icon: "ic_transport.svg",
          },
          {
            name: "Accomodation",
            rating: "Excellent",
            score: "4.7",
            icon: "ic_accomodation.svg",
          },
          {
            name: "Food",
            rating: "Excellent",
            score: "4.8",
            icon: "ic_food.svg",
          },
          {
            name: "Tour Operator",
            rating: "Excellent",
            score: "4.8",
            icon: "ic_tour.svg",
          },
        ],
      },
      reviews: [
        {
          name: "Ammad",
          createdAt: "Oct 10 , 2020",
          rating: 4,
          comment:
            "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Beatae laudantium dolor architecto a et perspiciatis dignissimos reiciendis nobis voluptatum. Laboriosam?",
          tripDate: "Feb 2020",
          likes: 12,
          dislikes: 3,
        },
        {
          name: "Robert",
          createdAt: "Sep 10 , 2020",
          rating: 5,
          comment:
            "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Beatae laudantium dolor architecto a et perspiciatis dignissimos reiciendis nobis voluptatum. Laboriosam?",
          tripDate: "Oct 2020",
          likes: 20,
          dislikes: 13,
        },
        {
          name: "Albert",
          createdAt: "Jan 21 , 2021",
          rating: 3,
          comment:
            "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Beatae laudantium dolor architecto a et perspiciatis dignissimos reiciendis nobis voluptatum. Laboriosam?",
          tripDate: "Feb 2020",
          likes: 12,
          dislikes: 8,
        },
      ],
      departures: [
        {
          start: { day: "Wednesday", date: "29 Sep , 2021" },
          end: { day: "Saturday", date: "7 Oct , 2021" },
          prices: { old: "$1,450", new: "$742" },
          language: "English",
        },

        {
          start: { day: "Wednesday", date: "29 Sep , 2021" },
          end: { day: "Saturday", date: "7 Oct , 2021" },
          prices: { old: "$1,450", new: "$742" },
          language: "English",
        },

        {
          start: { day: "Wednesday", date: "29 Sep , 2021" },
          end: { day: "Saturday", date: "7 Oct , 2021" },
          prices: { old: "$1,450", new: "$742" },
          language: "English",
        },
      ],
    };
  },
  methods: {},
};
</script>


<style lang="scss">
.home {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;

  .top-bar {
    width: 100%;

    border-bottom: 0.1rem solid var(--clr-border);
    display: flex;
    justify-content: center;
    padding: 1rem 0rem;

    .inner {
      height: 100%;
      width: var(--content-width);
      transition: var(--transition);
      display: flex;
      align-items: center;

      img {
        max-width: 25rem;
      }
    }
  }

  .content {
    height: 100%;
    width: var(--content-width);
    transition: var(--transition);
    padding-top: 2rem;

    .top-info-container {
      width: 100%;
      display: grid;
      grid-template-columns: 60% 40%;

      .img-book-container {
        display: flex;
        flex-direction: column;
      }

      .details-container {
        display: flex;
        flex-direction: column;
        padding: 0rem 3rem;
        align-items: flex-start;

        .green-tag {
          background: #319380;
          color: white;
          font-weight: 700;
          font-size: 1.4rem;
          border-radius: 1rem;
          padding: 0.1rem 0.6rem;
          margin-bottom: 1rem;
        }

        .title {
          font-size: 3.2rem;
          letter-spacing: -0.6px;
          font-weight: 700;
          margin-bottom: 1.4rem;
        }

        .days-rating-cont {
          font-size: 1.6rem;
          letter-spacing: 0.2px;
          line-height: 1.25px;
          font-weight: 700;
          display: flex;
          align-items: center;
          margin-bottom: 1rem;

          img {
            width: 2rem;
          }

          .count {
            color: #818d99;
            font-weight: 400;
          }
        }

        .start-end-cont {
          font-size: 1.6rem;
          margin-bottom: 2rem;
        }

        .tags {
          display: flex;
          flex-wrap: wrap;
          margin-bottom: 2rem;

          .tag {
            font-size: 1.4rem;
            line-height: 2.1rem;
            border-radius: 0.7rem;
            padding: 0.2rem 0.8rem;
            margin-right: 0.8rem;
            margin-bottom: 0.8rem;
            color: #415466;
            background: #ebeef2;
          }
        }

        .kv-container {
          width: 100%;
          display: grid;
          grid-template-columns: 1fr 1fr;
          gap: 2rem;
          margin-bottom: 2rem;

          .kv {
            display: flex;
            flex-direction: column;

            .key {
              font-weight: 700;
              font-size: 1.6rem;
              text-overflow: ellipsis;
              overflow: hidden;
            }

            .val {
              font-weight: 700;
              font-size: 1.6rem;
              text-overflow: ellipsis;
              overflow: hidden;
              font-size: 1.6rem;
              margin-top: 1rem;
              color: #2c3e50;
              font-weight: 400;
            }
          }
        }

        .card {
          width: 100%;
          box-shadow: var(--card-shadow);
          padding: 2.4rem;
          display: flex;
          flex-direction: column;
          border-radius: 1.2rem;

          .discount-container {
            font-size: 1.4rem;
            color: #2c3e50;

            .percent {
              line-height: 2rem;
              font-weight: 700;
              background-color: #e74c3c;
              color: #fff;
              border-radius: 1rem;
              padding: 0 0.6rem;
              margin-left: 0.4rem;
            }
          }

          .price-container {
            margin-top: 0.4rem;
            margin-bottom: 2rem;
            .currency {
              text-transform: uppercase;
              font-size: 2rem;
              display: inline-block;
              letter-spacing: -0.2px;
              font-weight: 700;
              margin-right: 0.4rem;
            }
            .amount {
              font-size: 4rem;
              line-height: 4.8rem;
              font-weight: 700;
            }
          }

          .actions-container {
            display: flex;
            margin-bottom: 2rem;

            .check {
              width: 100%;
              height: 5rem;
              background: #0a7bbd;
              border: none;
              font-weight: 700;
              text-align: center;
              font-family: Helvetica Neue, Arial, Helvetica, Geneva, FreeSans,
                sans-serif;
              font-size: 1.6rem;
              color: white;
              border-radius: 0.4rem;
              transition: var(--transition);

              &:hover {
                background: #085886;
              }
            }

            img {
              height: 5rem;
              widows: 5rem;
              margin-left: 2rem;
              box-shadow: var(--card-shadow);
              border-radius: 50%;
              padding: 0.6rem;
              transition: var(--transition);

              &:hover {
                box-shadow: 0rem 0rem 1rem 0rem lightgray;
              }
            }
          }

          .extra {
            display: flex;
            margin-bottom: 1rem;

            img {
              width: 2rem;
              height: 2rem;
              margin-right: 1rem;
            }

            span {
              font-size: 1.4rem;
              line-height: 2rem;
            }
          }
        }
      }
    }

    .places-container {
      width: 60%;
      display: flex;
      flex-direction: column;
      margin-top: -28rem;
      .planning-container {
        width: 100%;
        height: 5.4rem;
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        gap: 0.5rem;
        box-shadow: var(--card-shadow);
        border-radius: 1rem;
        margin-top: 2rem;
        margin-bottom: 3rem;
        padding: 0rem 2.4rem;
        font-size: 1.6rem;
        align-items: center;
      }

      .heading {
        font-size: 2.8rem;
        font-weight: 700;
        margin-top: 2rem;
      }

      .overview {
        font-size: 1.4rem;
        color: #2c3e50;
        font-family: sans-serif;
        margin-top: 1rem;
      }

      .highlights {
        width: 100%;
        display: flex;
        flex-direction: column;
        margin-top: 2rem;
        margin-bottom: 2rem;
        .highlight {
          width: 100%;
          display: flex;
          font-size: 1.6rem;
          margin-bottom: 1.4rem;
          align-items: center;

          img {
            width: 2.4rem;
            height: 2.4rem;
            margin-right: 1rem;
          }
        }
      }

      .features {
        width: 100%;
        margin-top: 3rem;
        margin-bottom: 3rem;
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 3rem;
        .feature {
          width: 100%;
          display: flex;
          flex-direction: row;

          img {
            width: 2.4rem;
            height: 2.4rem;
            margin-right: 1rem;
          }

          .info {
            width: 100%;
            display: flex;
            flex-direction: column;
            .title {
              font-size: 1.6rem;
              font-weight: 700;
              line-height: 2.4rem;
            }
            .desc {
              font-size: 1.4rem;
              margin-top: 0.5rem;
            }
          }
        }
      }

      .download-brochure {
        margin-top: 5rem;
        width: 100%;
        padding: 2rem;
        box-shadow: var(--card-shadow);
        display: flex;

        img {
          width: 3.2rem;
          height: 3.2rem;
          margin-right: 1rem;
        }

        .info {
          width: 100%;
          display: flex;
          flex-direction: column;
          .title {
            font-weight: 700;
            font-size: 2rem;
          }
          .desc {
            margin-top: 0.4rem;
            font-size: 1.6rem;
          }
        }
      }

      .policy-container {
        width: 100%;
        padding: 2rem 3rem;
        background: #f3f8fc;
        display: flex;
        flex-direction: column;
        margin: 3rem 0rem;

        button {
          height: 4rem;
          margin-right: auto;
          margin-top: 2.4rem;
          padding: 0.4rem 1.2rem;
        }

        .banner {
          margin-right: auto;
          border-radius: 2rem;
          padding: 0.4rem 0.8rem;
          background: #085786;
          color: white;
          font-size: 1.2rem;
          line-height: 1.8rem;
        }

        .title {
          margin-top: 1.4rem;
          font-size: 2rem;
          font-weight: 700;
        }

        .policies {
          margin-top: 2.2rem;
          width: 100%;
          display: grid;
          grid-template-columns: 1fr 1fr 1fr;

          .policy {
            width: 100%;
            display: flex;
            flex-direction: column;
            gap: 1rem;

            img {
              width: 2.4rem;
              height: 2.4rem;
            }

            .title {
              font-size: 1.6rem;
              font-weight: 700;
            }

            .desc {
              font-size: 1.4rem;
              font-weight: 400;
            }
          }
        }
      }

      .stays {
        width: 100%;
        display: flex;
        flex-direction: column;
        margin-top: 1rem;
        margin-bottom: 4rem;

        .stay {
          width: 100%;
          display: flex;
          align-items: center;
          font-size: 2rem;
          font-weight: 700;
          border-bottom: 0.1rem solid lightgray;
          padding: 2rem 0rem;

          img {
            width: 5.6rem;
            height: 5.6rem;
            background: rgba(102, 176, 218, 0.1);
            margin-right: 2rem;
            padding: 1.4rem;
            border-radius: 0.4rem;
          }
        }
      }

      .credit-cards {
        display: flex;
        align-items: center;
        color: gray;
        font-size: 1.4rem;
        margin-top: 1.4rem;

        img {
          height: 2rem;
          margin-left: 1.5rem;
        }
      }

      .availability-container {
        width: 100%;
        display: flex;
        flex-direction: column;
        margin-top: 2rem;

        .days {
          font-size: 1.4rem;
          color: gray;
          font-weight: 300;
        }

        .title {
          font-size: 1.8rem;
          font-weight: 700;
          margin: 0.5rem 0rem;
        }

        .dest {
          color: gray;
          font-size: 1.6rem;
          font-weight: 300;
        }

        .tour-actions {
          display: flex;
          margin-top: 2rem;

          .action {
            display: flex;
            flex-direction: row;
            align-items: center;
            font-size: 1.6rem;
            border: 0.1rem solid #2c3e50;
            color: #2c3e50;
            padding: 0.8rem 1.4rem;
            border-radius: 2rem;

            img {
              filter: brightness(1) invert(1);
              width: 1.8rem;
              margin-right: 1rem;
            }
          }

          .selected {
            background: #2c3e50;
            color: white;

            img {
              filter: brightness(1) invert(0);
            }
          }

          :first-child {
            margin-right: 2rem;
          }
        }

        .group-availability {
          .cards {
            width: 100%;
            display: grid;
            grid-template-columns: 1fr 1fr;
            margin-top: 2rem;
            padding: 1rem 0rem;
            margin-bottom: 3rem;

            .card {
              width: 95%;
              box-shadow: var(--card-shadow);
              display: flex;
              flex-direction: column;
              padding: 2rem;

              img {
                width: 2rem;
                height: 2rem;
                margin-bottom: 1rem;
              }

              .title {
                font-size: 1.6rem;
                font-weight: 700;
              }

              .desc {
                font-size: 1.4rem;
                font-weight: 400;
              }
            }
          }

          .sub-heading {
            font-size: 1.7rem;
            font-weight: 700;
          }
          .dates-container {
            display: flex;
            flex-direction: row;
            margin-top: 1rem;
            margin-bottom: 3rem;

            button {
              font-size: 1.6rem;
              padding: 2rem;
              border-radius: 1rem;
              background: transparent;
              border: 0.1rem solid #2c3e50;
              color: #2c3e50;
              margin-right: 1rem;
            }

            .selected {
              background: #2c3e50;
              color: white;
              font-weight: 700;
            }

            :last-child {
              margin-right: 0rem !important;
            }
          }

          .departures {
            width: 100%;
            display: flex;
            flex-direction: column;
            margin-top: 2rem;

            .departure {
              width: 100%;
              display: flex;
              flex-direction: row;
              padding: 2rem;
              box-shadow: 0rem 0rem 1rem 0rem lightgray;
              margin-bottom: 2rem;

              .top {
                width: 100%;

                display: grid;
                grid-template-columns: 1fr 4rem 1fr 1fr;

                gap: 2rem;

                .dates {
                  width: 100%;
                  display: flex;
                  flex-direction: column;

                  .day {
                    font-size: 1.4rem;
                    color: gray;
                  }
                  .date {
                    font-size: 1.6rem;
                    font-weight: 700;
                    color: black;
                  }
                }

                img {
                  width: 2rem;
                  height: 2rem;
                  margin-right: 2rem;
                }

                .prices {
                  display: flex;
                  flex-direction: column;

                  .old {
                    font-size: 1.4rem;
                    color: gray;
                  }
                  .new {
                    font-size: 1.6rem;
                    color: black;
                    font-weight: 700;
                  }
                }
              }

              .confirm {
                width: 20rem;
                height: 4rem;
                background: #0a7bbd;
                color: white;
                border: none;
                font-size: 1.4rem;
                font-weight: 700;
                border-radius: 0.4rem;
              }
            }
          }
        }
      }
    }
  }
}

@media screen and (max-width: 1080px) {
  :root {
    --content-width: 100%;
  }

  .home {
    .top-bar {
      .inner {
        padding: 2rem;
      }
    }

    .content {
      padding-top: 0rem;
      .img-book-container {
        padding: 2rem;
      }
      .top-info-container {
        grid-template-columns: 1fr;
      }

      .places-container {
        width: 100%;
        padding: 0rem 2rem;
        margin-top: 0rem;
      }
    }
  }
}

@media screen and (max-width: 480px) {
  :root {
    --content-width: 100%;
  }

  .home {
    .content {
      .details-container {
        padding: 0rem 2rem !important;
      }
      .planning-container {
        padding-top: 2rem !important;
        padding-bottom: 2rem !important;
        grid-template-columns: 1fr !important;
        height: auto !important;
        gap: 1rem !important;
        justify-content: left !important;
      }
    }

    .download-brochure {
      display: grid !important;

      img {
        width: 2rem !important;
        height: 2rem !important;
      }
      .info {
        margin: 2rem 0rem;
      }

      .hollow-btn {
        min-width: 100% !important;
        font-size: 1.4rem;
        height: 4rem;
      }
    }

    .policy-container {
      .policies {
        grid-template-columns: 1fr !important;
        gap: 3rem;

        .policy {
          display: grid !important;
          grid-template-columns: 4rem 1fr !important;

          img {
            margin-top: 1rem;
          }

          .title {
            margin: 0.2rem !important;
          }

          .desc {
            margin-top: -2rem;
            grid-column-end: 3;
            margin-left: 0.4rem;
          }
        }
      }

      .hollow-btn {
        margin: 0 !important;
        width: 100% !important;
        margin-top: 2rem !important;
      }
    }
    .group-availability {
      .cards {
        grid-template-columns: 1fr !important;
        gap: 2rem;
      }

      .dates-container {
        width: 100%;
        overflow: scroll;

        button {
          font-size: 1.2rem !important;
          padding: 1rem !important;
        }
      }

      .departure {
        width: 100%;
        flex-direction: column !important;

        .top {
          grid-template-columns: 1fr 4rem 1fr !important;
          gap: 1rem;

          img {
            margin-top: 1rem;
          }
          .lang-container {
            grid-column-start: 3;
          }
        }

        .confirm {
          width: 100% !important;
          height: 4rem;
          margin-top: 2rem;
        }
      }
    }
  }
}
</style>

