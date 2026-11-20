import { useEffect, useState } from "react";
import { Link } from "react-router-dom";
import { destinations, tours } from "./data";

function SEO({ title, description }) {
  useEffect(() => {
    document.title = `${title} | Explore Afghanistan`;

    let meta = document.querySelector('meta[name="description"]');

    if (meta) {
      meta.setAttribute("content", description);
    }
  }, [title, description]);

  return null;
}

function SectionHeading({ subtitle, title, description }) {
  return (
    <div className="section-heading">
      <span>{subtitle}</span>
      <h2>{title}</h2>
      <p>{description}</p>
    </div>
  );
}

function DestinationCard({ item }) {
  return (
    <article className="destination-card">
      <img src={item.image} alt={`${item.name} landscape`} />

      <div className="card-content">
        <span className="category">{item.category}</span>
        <h3>{item.name}</h3>
        <p>{item.description}</p>
        <span className="province">{item.province}, Afghanistan</span>
      </div>
    </article>
  );
}

function TourCard({ item }) {
  return (
    <article className="tour-card">
      <img src={item.image} alt={`${item.name} scenery`} />

      <div className="card-content">
        <span className="category">{item.type} Experience</span>
        <h3>{item.name}</h3>
        <p>{item.description}</p>
        <div className="tour-bottom">
          <span>◷ {item.duration}</span>
          <Link to="/contact">Enquire Now →</Link>
        </div>
      </div>
    </article>
  );
}

// PAGE 1: HOME

export function Home() {
  return (
    <>
      <SEO
        title="Discover Afghanistan"
        description="Explore Afghanistan's destinations, culture, historical landmarks, and natural landscapes."
      />

      <section className="hero">
        <div className="hero-overlay">
          <div className="container hero-content">
            <span className="hero-label">
              DISCOVER THE HEART OF CENTRAL ASIA
            </span>

            <h1>
              Discover the
              <br />
              Beauty of <span>Afghanistan</span>
            </h1>

            <p>
              Explore remarkable landscapes, ancient heritage,
              rich traditions, and unforgettable destinations.
            </p>

            <div className="hero-buttons">
              <Link to="/destinations" className="primary-button">
                Explore Destinations →
              </Link>

              <Link to="/about" className="outline-button">
                Discover Our Story
              </Link>
            </div>
          </div>
        </div>
      </section>

      <section className="stats-section">
        <div className="container stats-grid">
          <div>
            <h2>34</h2>
            <p>Provinces</p>
          </div>

          <div>
            <h2>3000+</h2>
            <p>Years of History</p>
          </div>

          <div>
            <h2>100+</h2>
            <p>Places to Discover</p>
          </div>

          <div>
            <h2>1</h2>
            <p>Unique Heritage</p>
          </div>
        </div>
      </section>

      <section className="section container">
        <SectionHeading
          subtitle="EXPLORE THE COUNTRY"
          title="Popular Destinations"
          description="Discover some of Afghanistan's remarkable places."
        />

        <div className="destination-grid">
          {destinations.slice(0, 3).map((item) => (
            <DestinationCard key={item.id} item={item} />
          ))}
        </div>

        <div className="center-button">
          <Link to="/destinations" className="primary-button">
            View All Destinations →
          </Link>
        </div>
      </section>

      <section className="feature-section">
        <div className="container feature-grid">
          <div>
            <span className="category">A LAND OF HERITAGE</span>
            <h2>A Country of Extraordinary Stories</h2>
            <p>
              Afghanistan has a rich history shaped by centuries
              of cultural exchange, traditional craftsmanship,
              architecture, and diverse landscapes.
            </p>

            <Link to="/about" className="primary-button">
              Learn More →
            </Link>
          </div>

          <img
            src="https://images.unsplash.com/photo-1470770841072-f978cf4d019e?w=1000"
            alt="Mountain lake landscape"
          />
        </div>
      </section>

      <section className="section container">
        <SectionHeading
          subtitle="TRAVEL EXPERIENCES"
          title="Explore Our Tours"
          description="Find inspiration for cultural and nature experiences."
        />

        <div className="tour-grid">
          {tours.map((item) => (
            <TourCard key={item.id} item={item} />
          ))}
        </div>
      </section>

      <section className="cta-section">
        <h2>Your Afghanistan Journey Starts Here</h2>
        <p>Discover destinations and learn more about the country.</p>
        <Link to="/contact" className="primary-button">
          Contact Us →
        </Link>
      </section>
    </>
  );
}

// PAGE 2: DESTINATIONS

export function Destinations() {
  const [search, setSearch] = useState("");
  const [category, setCategory] = useState("All");

  const filtered = destinations.filter((item) => {
    const matchesSearch =
      item.name.toLowerCase().includes(search.toLowerCase()) ||
      item.province.toLowerCase().includes(search.toLowerCase());

    const matchesCategory =
      category === "All" || item.category === category;

    return matchesSearch && matchesCategory;
  });

  return (
    <>
      <SEO
        title="Afghanistan Destinations"
        description="Discover Afghanistan destinations including Bamyan, Herat, Kabul, Badakhshan, and more."
      />

      <section className="page-hero destinations-hero">
        <div>
          <span>DISCOVER BEAUTIFUL PLACES</span>
          <h1>Explore Destinations</h1>
          <p>Discover the remarkable places of Afghanistan.</p>
        </div>
      </section>

      <section className="section container">
        <SectionHeading
          subtitle="FIND YOUR NEXT DESTINATION"
          title="Places Worth Discovering"
          description="Search and explore destinations by name or category."
        />

        <div className="filter-area">
          <input
            type="search"
            placeholder="Search destination or province..."
            value={search}
            onChange={(e) => setSearch(e.target.value)}
          />

          <select
            value={category}
            onChange={(e) => setCategory(e.target.value)}
          >
            <option>All</option>
            <option>Nature</option>
            <option>History</option>
            <option>Culture</option>
            <option>City</option>
          </select>
        </div>

        <div className="destination-grid">
          {filtered.map((item) => (
            <DestinationCard key={item.id} item={item} />
          ))}
        </div>

        {filtered.length === 0 && (
          <p className="no-results">No destinations found.</p>
        )}
      </section>
    </>
  );
}

// PAGE 3: TOURS

export function Tours() {
  return (
    <>
      <SEO
        title="Afghanistan Tours"
        description="Explore cultural and nature tour ideas and travel experiences in Afghanistan."
      />

      <section className="page-hero tours-hero">
        <div>
          <span>EXPERIENCE SOMETHING DIFFERENT</span>
          <h1>Tours & Experiences</h1>
          <p>Explore the country's history, culture, and nature.</p>
        </div>
      </section>

      <section className="section container">
        <SectionHeading
          subtitle="EXPLORE WITH PURPOSE"
          title="Discover Travel Experiences"
          description="Browse our sample tour ideas and contact us for more information."
        />

        <div className="tour-grid">
          {tours.map((item) => (
            <TourCard key={item.id} item={item} />
          ))}
        </div>

        <div className="travel-notice">
          <h3>Important Travel Information</h3>
          <p>
            These are sample travel experiences, not confirmed bookings.
            Travel conditions, permissions, availability, and safety
            should be checked with reliable current sources before
            making any travel arrangements.
          </p>
        </div>
      </section>
    </>
  );
}

// PAGE 4: ABOUT

export function About() {
  return (
    <>
      <SEO
        title="About Afghanistan"
        description="Learn about Afghanistan's history, culture, heritage, traditions, and geography."
      />

      <section className="page-hero about-hero">
        <div>
          <span>OUR COUNTRY, OUR HERITAGE</span>
          <h1>About Afghanistan</h1>
          <p>A land with a rich history and diverse cultural heritage.</p>
        </div>
      </section>

      <section className="section container">
        <div className="about-grid">
          <div>
            <span className="category">A RICH CULTURAL HERITAGE</span>
            <h2>Discover Afghanistan</h2>

            <p>
              Afghanistan is a landlocked country in Central and
              South Asia. Its geography includes high mountains,
              valleys, plains, and deserts.
            </p>

            <p>
              The country has a long history and diverse communities.
              Its cultural heritage can be seen in traditional music,
              poetry, architecture, handicrafts, and food.
            </p>

            <p>
              From the historic cities to the mountain landscapes,
              Afghanistan offers many subjects to explore and learn about.
            </p>
          </div>

          <img
            src="https://images.unsplash.com/photo-1464822759023-fed622ff2c3b?w=1000"
            alt="Mountain landscape"
          />
        </div>
      </section>

      <section className="culture-section">
        <div className="container">
          <SectionHeading
            subtitle="THE AFGHAN WAY OF LIFE"
            title="Culture & Traditions"
            description="Explore important elements of Afghanistan's cultural heritage."
          />

          <div className="culture-grid">
            <div className="culture-card">
              <span>01</span>
              <h3>Traditional Food</h3>
              <p>
                Discover dishes such as Kabuli Pulao, Mantu,
                Ashak, and traditional bread.
              </p>
            </div>

            <div className="culture-card">
              <span>02</span>
              <h3>Arts & Crafts</h3>
              <p>
                Explore carpets, embroidery, pottery,
                and traditional craftsmanship.
              </p>
            </div>

            <div className="culture-card">
              <span>03</span>
              <h3>Languages</h3>
              <p>
                Dari and Pashto are the official languages
                of Afghanistan, alongside other languages.
              </p>
            </div>

            <div className="culture-card">
              <span>04</span>
              <h3>Historical Heritage</h3>
              <p>
                Learn about historic cities, monuments,
                architecture, and cultural landmarks.
              </p>
            </div>
          </div>
        </div>
      </section>
    </>
  );
}

// PAGE 5: CONTACT

export function Contact() {
  const [submitted, setSubmitted] = useState(false);

  function handleSubmit(e) {
    e.preventDefault();
    setSubmitted(true);
  }

  return (
    <>
      <SEO
        title="Contact Explore Afghanistan"
        description="Contact Explore Afghanistan for information and travel enquiries."
      />

      <section className="page-hero contact-hero">
        <div>
          <span>WE WOULD LOVE TO HEAR FROM YOU</span>
          <h1>Contact Us</h1>
          <p>Send us your questions and enquiries.</p>
        </div>
      </section>

      <section className="section container contact-layout">
        <div className="contact-info">
          <span className="category">GET IN TOUCH</span>
          <h2>Let's Start a Conversation</h2>

          <p>
            Have a question about Afghanistan or our sample
            travel experiences? Send us a message.
          </p>

          <div className="contact-item">
            <strong>Website</strong>
            <span>Explore Afghanistan</span>
          </div>

          <div className="contact-item">
            <strong>Location</strong>
            <span>Afghanistan</span>
          </div>

          <div className="contact-item">
            <strong>Enquiries</strong>
            <span>Use the contact form</span>
          </div>
        </div>

        <form className="contact-form" onSubmit={handleSubmit}>
          <h2>Send a Message</h2>

          <label>Your Name</label>
          <input
            type="text"
            placeholder="Enter your name"
            required
          />

          <label>Email Address</label>
          <input
            type="email"
            placeholder="Enter your email"
            required
          />

          <label>Subject</label>
          <input
            type="text"
            placeholder="What is your enquiry about?"
            required
          />

          <label>Your Message</label>
          <textarea
            rows="5"
            placeholder="Write your message..."
            required
          />

          <button type="submit" className="primary-button">
            Send Message →
          </button>

          {submitted && (
            <p className="form-message">
              Thank you! This demo form has received your submission
              locally, but it has not sent or saved your message.
            </p>
          )}
        </form>
      </section>
    </>
  );
}