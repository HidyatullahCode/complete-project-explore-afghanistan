import { Link, NavLink, Outlet } from "react-router-dom";

export default function Layout() {
  return (
    <>
      <header className="header">
        <div className="container navbar">
          <Link to="/" className="logo">
            <span className="logo-icon">✦</span>
            Explore<span>Afghanistan</span>
          </Link>

          <nav className="nav-links">
            <NavLink to="/">Home</NavLink>
            <NavLink to="/destinations">Destinations</NavLink>
            <NavLink to="/tours">Tours</NavLink>
            <NavLink to="/about">About</NavLink>
            <NavLink to="/contact">Contact</NavLink>
          </nav>

          <Link to="/contact" className="nav-button">
            Plan Your Trip
          </Link>
        </div>
      </header>

      <main>
        <Outlet />
      </main>

      <footer className="footer">
        <div className="container footer-grid">
          <div>
            <Link to="/" className="logo footer-logo">
              ✦ Explore<span>Afghanistan</span>
            </Link>
            <p>
              Discover the landscapes, culture, history, and heritage
              of Afghanistan.
            </p>
          </div>

          <div>
            <h3>Explore</h3>
            <Link to="/destinations">Destinations</Link>
            <Link to="/tours">Tours</Link>
            <Link to="/about">About Afghanistan</Link>
          </div>

          <div>
            <h3>Information</h3>
            <Link to="/contact">Contact Us</Link>
            <Link to="/about">Our Story</Link>
          </div>
        </div>

        <div className="copyright">
          © {new Date().getFullYear()} Explore Afghanistan. All rights reserved.
        </div>
      </footer>
    </>
  );
}